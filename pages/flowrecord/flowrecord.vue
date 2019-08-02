<template>
	<view class="container">
		<view class="flow_item clearfix flex flexCenter" v-for="(item,index) in my_flow" :key="index">
			<view style="width: 100%;height: 30rpx;"></view>
			<view class="item flex">	
				<view class="iteminfo flex">
					<view class="item_info_logo">
						<image class="my_icon" :src="item.flow_icon"></image>
					</view>
					<view class="item_info_name">
						<view class="my_name"><span>{{item.flow_name}}</span></view>
						<view style="width: 100%;height: 30rpx;"></view>
						<view class="flex">
							<view>积分 ： </view>
							<view class="num">{{item.flow_integral}}</view>
						</view>
					</view>
				</view>
				<view class="flex">
					<span class="my_time">{{item.flow_time}}</span>
					<view style="width: 30rpx;height: 100%;"></view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	
	export default {
		data() {
			return {
				my_flow: [
					{
						flow_icon:"../../static/images/about-img.png",
						flow_name:"快乐的猫",
						flow_integral:200,
						flow_time:"2019-05-30"
					},
					{
						flow_icon:"../../static/images/about-img.png",
						flow_name:"快乐的仔",
						flow_integral:500,
						flow_time:"2019-05-30"
					},
					{
						flow_icon:"../../static/images/about-img.png",
						flow_name:"许你一世无忧",
						flow_integral:800,
						flow_time:"2019-05-30"
					}
				]
			}
		},
	}
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{background: #F5F5F5;}
	.item{width: 690rpx;height: 160rpx;background: #FFFFFF;border-radius: 30rpx;box-sizing: border-box;justify-content: space-between;}
	.flow_item{width: 100%;flex-direction: column;}
	.my_icon{width: 120rpx;height: 120rpx;border-radius: 50%;margin-left: 30rpx;margin-right: 20rpx;}
	.item_info{height:100%;align-items: center;}
	.item_info_name{font-size: 26rpx;color: #212121;}
	.num{color: #FF556B;}
	.my_time{font-size: 24rpx;color: #666666;}
</style>
