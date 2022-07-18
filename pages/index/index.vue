<template>
	<view>
		<block v-for="(item,index) in list" :key="index">
			<CommonList :item='item' :index="index"></CommonList>
			<divider></divider>
		</block>
	</view>
</template>

<script>
	import CommonList from '@/components/common/common-list.vue'
	export default {
		data() {
			return {
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
							type:'support',
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

		},
		components:{
			CommonList
		}
	}
</script>

<style lang="scss" scoped>
	
</style>
