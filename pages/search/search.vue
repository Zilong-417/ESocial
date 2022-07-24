<template>
	<view>
		<!--搜索历史-->
		<view class="py-2 font-md px-2">搜索历史</view>
		<view class="flex flex-wrap">
			<view class="border rounded font mx-2 my-1 px-2" v-for="(item,index) in searchList" :key="index" hover-class="bg-light">我是测试数据</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				searchList:['我是测试数据','我是测试数据','我是测试数据','我是测试数据']
			}
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
