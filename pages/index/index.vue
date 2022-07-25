<template>
	<view>
		<!--导航栏-->
		<scroll-view scroll-x class="scroll-row border-bottom border-light-secondary sw" 
		:scroll-into-view="scrollInto" 
		scroll-with-animation>
			<view v-for="(item,index) in tabList" :key="index"
			class="scroll-row-item px-3 py-2 font-md" :id="'tab'+index"
			:class="tabIndex===index?'text-main font-lg font-weight-bold':''"
			@click="changeTab(index)">{{item.name}}</view>
		</scroll-view>
		<swiper :duration="125" :current="tabIndex" @change="onChangeTab" 
		:key="index" :style="'height:'+scrollH+'px'">
			<swiper-item v-for="(item,index) in newlist" :key="index">
				<scroll-view scroll-y :style="'height:'+scrollH+'px'" @scrolltolower="loadmore(index)">
					<template v-if="item.list.length>0">
						<block v-for="(item2,index2) in item.list" :key="index2">
							<CommonList :item='item2' :index="index2" @follow="follow" @doSupport='doSupport' ></CommonList>
							<divider></divider>
						</block>
						<!--加载栏-->
						<load-more :loadmore='item.loadmore'></load-more>
					</template>
					<!--没有数据-->
					<template v-else>
						
						<no-thing></no-thing>
					</template>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script> 

	const demo=[{
			username:'小龙',
			userpic:'../../static/default.jpg',
			newtime:'2022-7-18 下午15：28',
			isFollow:false,
			title:'标题',
			titlepic:'/static/demo/datapic/1.jpg',
			support:{
				type:'support',
				support_count:1,
				unsupport_count:2,
			},
			comment_count:2,
			share_num:90
			},
			{
				username:'小龙',
				userpic:'../../static/default.jpg',
				newtime:'2022-7-18 下午15：28',
				isFollow:false,
				title:'标题',
				titlepic:'/static/demo/datapic/1.jpg',
				support:{
					type:'support',
					support_count:1,
					unsupport_count:2,
				},
					comment_count:2,
					share_num:90
			}]
	import CommonList from '@/components/common/common-list.vue'
	import loadMore from '@/components/common/load-more.vue'
	export default {
		data() {
			return {
				//列表高度
				scrollH:600,
				scrollInto:'',
				tabIndex:0,
				tabList:[{
					name:'关注'
				},{
					name:'推荐'
				},{
					name:'体育'
				},{
					name:'热点'
				},{
					name:'财经'
				},{
					name:'娱乐'
				},{
					name:'军事'
				},{
					name:'历史'
				},{
					name:'本地'
				}],
				newlist:[]
			}
		},
		//监听点击导航栏跳转
		onNavigationBarSearchInputClicked() {
			uni.navigateTo({
				url:'../search/search'
			})
		},
		//监听点击导航栏按钮
		onNavigationBarButtonTap(){
			uni.navigateTo({
				url:'../add/add'
			})
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res) => {
					this.scrollH=res.windowHeight-uni.upx2px(100)
				}
			})
			this.getData()
		},
		methods: {
			getData(){
				var arr=[]
				for(let i=0;i<this.tabList.length;i++){
					var obj={
						//加载类型
						loadmore:'上拉加载更多',
						list:[],
						
					}
					if(i<3){
						obj.list=demo
					}
					arr.push(obj)
				}
				this.newlist=arr
			},
			//切换选项
			changeTab(index){
				if(this.tabIndex===index){
					return
				}
					this.tabIndex=index
					this.scrollInto='tab'+index
				
			},
			//点赞
			follow(index){
				//console.log(index)
				this.list[index].isFollow=true,
				uni.showToast({
					title:'关注成功'
				})
			},
			//顶踩操作
			doSupport(e){
				//console.log(e)
				let item=this.list[e.index]
				//之前没有操作过
				if(item.support.type===''){
					item.support.type=e.type
					item.support[e.type+'_count']++
					return;
				}
				else if(item.support.type==='support'&&e.type==='unsupport'){
					item.support.support_count--
					item.support.unsupport_count++
				}
				else if(item.support.type==='unsupport'&&e.type==='support'){
					item.support.support_count++
					item.support.unsupport_count--
				}
				item.support.type=e.type
			},
			//监听滑动
			onChangeTab(e){
				this.changeTab(e.detail.current)
			},
			//上拉加载
			loadmore(index){
				//拿到当前列表
				let item=this.newlist[index]
				//判断是否处于可加载状态
				if(item.loadmore!=='上拉加载更多') return
				//模拟当前列表加载状态
				item.loadmore="正在加载中...",
				//模拟数据请求
				setTimeout(()=>{
					//加载数据
					item.list=[...item.list,...item.list]
					//恢复加载状态
					item.loadmore="上拉加载更多"
				},2000)
			}
		},
		components:{
			CommonList,
			loadMore
		}
	}
</script>

<style lang="scss" scoped>
	.sw{
		height: 100rpx;
	}
</style>
