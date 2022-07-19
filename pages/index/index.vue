<template>
	<view>
		<!--导航栏-->
		<scroll-view scroll-x class="scroll-row border-bottom border-light-secondary" :scroll-into-view="scrollInto" scroll-with-animation>
			<view v-for="(item,index) in tabList" :key="index"
			class="scroll-row-item px-3 py-2 font-md" :id="'tab'+index"
			:class="tabIndex===index?'text-main font-lg font-weight-bold':''"
			@click="changeTab(index)">{{item.name}}</view>
			
		</scroll-view>
		<!-- <block v-for="(item,index) in list" :key="index">
			<CommonList :item='item' :index="index" @follow="follow" @doSupport='doSupport' ></CommonList>
			<divider></divider>
		</block> -->
	</view>
</template>

<script>
	import CommonList from '@/components/common/common-list.vue'
	export default {
		data() {
			return {
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
				list:[
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
					},
					{
						username:'小龙',
						userpic:'../../static/default.jpg',
						newtime:'2022-7-18 下午15：28',
						isFollow:false,
						title:'标题',
						titlepic:'',
						support:{
							type:'unsupport',
							support_count:1,
							unsupport_count:2,
							
						},
						comment_count:2,
						share_num:90
					}
				]
			}
		},
		onLoad() {

		},
		methods: {
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
			}
		},
		components:{
			CommonList
		}
	}
</script>

<style lang="scss" scoped>
	
</style>
