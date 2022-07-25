<template>
	<view>
		<template v-if="searchedList.length===0">
			<!--搜索历史-->
			<view class="py-2 font-md px-2">搜索历史</view>
			<view class="flex flex-wrap">
				<view class="border rounded font mx-2 my-1 px-2" 
				v-for="(item,index) in searchList" 
				:key="index" hover-class="bg-light"
				@click="clickSearchHistory(item)">{{item}}</view>
			</view>
		</template>
		<template v-else>
			<!--搜索结果-->
			<block v-for="(item,index) in searchedList" :key="index">
				<common-list :item='item' :index="index" ></common-list>
			</block>
		</template>
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
			
	import commonList from "@/components/common/common-list.vue"
	export default {
		data() {
			return {
				searchText:'',//导航栏输入内容
				searchList:['我是测试数据','我是测试数据','我是测试数据','我是测试数据'],
				searchedList:[]
			}
		},
		components:{
			commonList
		},
		//导航栏改变触发的监听
		onNavigationBarSearchInputChanged(e){
			this.searchText=e.text
		},
		//导航栏按钮监听
		onNavigationBarButtonTap(e){
			this.searchEvent()
		},
		methods: {
			//点击搜索历史
			clickSearchHistory(text){
				this.searchText=text,
				this.searchEvent()
			},
			//搜索事件
			searchEvent(){
				//收起键盘
				uni.hideKeyboard(),
				//显示加载中
				uni.showLoading({
					title: '加载中....',
					mask: true
				});
				//请求搜索
				setTimeout(()=>{
					this.searchedList=demo,
					//隐藏加载
					uni.hideLoading()
				},3000)
			}
		}
	}
</script>

<style>

</style>
