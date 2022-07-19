<template>
	<!--列表样式-->
	<view class="p-2">
		<!--头像昵称|关注按钮-->
		<view class="flex align-center justify-between" >
			<view class="flex align-center" >
				<!--头像-->
				<image class="rounded-circle mr-2" 
				:src="item.userpic" 
				style="width: 65rpx;height: 65rpx;" 
				lazy-load ></image>
				<!--昵称,发布时间-->
				<view>
					<view class="font" style="line-height: 1.5;">{{item.username}}</view>
					<text  class="font-sm " style="color: #9D9589;
					line-height: 1.5;">{{item.newtime}}</text>
				</view>
			</view>
			<!--按钮-->
			<view class="flex align-center justify-center rounded bg-main text-white animated faster" 
			style="width: 90rpx;height: 50rpx;" hover-class="jello" @click="follow">
				关注
			</view>
			</view>
			<!--标题-->
			<view style="font-size: 30rpx;margin: 10rpx 0;">
				{{item.title}}
			</view>
			<!--图片-->
			<image v-if="item.titlepic" :src="item.titlepic" 
			class="rounded"
			style="height: 350rpx;width: 100%;"></image>
			<!--图标按钮-->
			<view class="flex align-center">
				<!--顶-->
				<view class="flex align-center justify-center flex-1 animated faster" hover-class="jello" @click="doSupport('support')"
				:class="item.support.type==='support'?'text-main':''">
					<text class="iconfont icon-dianzan2 mr-2" ></text>
					<text>{{item.support.support_count>0?item.support.support_count:'赞'}}</text>
				</view>
				<!--踩-->
				<view class="flex align-center justify-center flex-1 animated faster" hover-class="jello" @click="doSupport('unsupport')"
				:class="item.support.type==='unsupport'?'text-main':''">
					<text class="iconfont icon-cai mr-2" ></text>
					<text>{{item.support.unsupport_count>0?item.support.unsupport_count:'踩'}}</text>
				</view>
				<!--评论数-->
				<view class="flex align-center justify-center flex-1 animated faster" hover-class="jello">
					<text class="iconfont icon-pinglun2 mr-2" ></text>
					<text>{{item.comment_count>0?item.comment_count:'评论'}}</text>
				</view>
				<!--分享数-->
				<view class="flex align-center justify-center flex-1 animated faster" hover-class="jello" >
					<text class="iconfont icon-fenxiang mr-2" ></text>
					<text>{{item.share_num>0?item.share_num:'分享'}}</text>
				</view>
			</view>
		
		
	</view>
</template>

<script>
	export default{
			
		props:{
			item:Object,
			index:Number
		},
		methods:{
			//关注
			follow(index){
				this.$emit('follow',this.index)
			},
			//点赞
			doSupport(type){
				this.$emit('doSupport',{
					type,
					index:this.index
				})
			},
		}
	}
	
	
</script>

<style>
</style>