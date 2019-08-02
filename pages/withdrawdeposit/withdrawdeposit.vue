<template>
	<view class="container">
		<view style="width: 100%;height: 50rpx;"></view>
		<view class="container_header">
			<view class="container_header_box flex" @click="webself.$Router.navigateTo({route:{path:'/pages/cashaccount/cashaccount'}})">
				<view>去绑定银行卡</view>
				<view><image style="width: 12rpx;height: 22rpx;" src="../../static/images/about-icon8.png"></image></view>
			</view>
		</view>
		<view style="width: 100%;height: 150rpx;"></view>
		<view class="container_content">
			<view style="width: 100%;height: 50rpx;"></view>
			<view class="container_content_title">提现金额</view>
			<view style="width: 100%;height: 80rpx;"></view>
			<view class="container_content_num flex">
				<view class="icon_img">￥</view>
				<view class="icon_num"><input class="money_txt" type="text"></view>
			</view>
			<view style="width: 100%;height: 20rpx;"></view>
			<view class="container_content_explain flex">
				<view class="container_content_explain_left">本次可提现佣金200元</view>
				<view class="alldeposit">全部提现</view>
			</view>
			<view style="width: 100%;height: 120rpx;"></view>
				<view class="confirm flex flexCenter">
				<view class="confirm_box">提现</view>
			</view>
			<view style="width: 100%;height: 60rpx;"></view>
		</view>
	</view>
</template>

<script>
	
	export default {
		components: {
			
		},
		data() {
			return {
				webself:this
			}
		},
		methods: {
			
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{background: #F5F5F5;}
	.container{padding: 0 30rpx;}
	.container_header_box{width: 630rpx;height: 100rpx;background: #FFFFFF;justify-content: space-between;padding: 0 30rpx;border-radius: 20rpx;}
	.container_content{width: 610rpx;height: 510rpx;background: #FFFFFF;padding: 0 40rpx;border-radius: 20rpx;}
	.container_content_title{font-size: 28rpx;color: #222222;line-height: 28rpx;}
	.icon_img{font-size: 60rpx;color: #222222;line-height: 60rpx;}
	.container_content_num{border-bottom: solid 1px #EAEAEA;}
	.icon_num{width: 100%;flex: 1;}
	.money_txt{width: 100%;}
	.container_content_explain{justify-content: space-between;font-size: 24rpx;line-height: 24rpx;}
	.container_content_explain_left{color: #222222;opacity: .6;}
	.alldeposit{color: #FF556B;}
	.confirm_box{width: 600rpx;height: 80rpx;background: #FF566D;color: #FFFFFF;text-align: center;line-height: 80rpx;font-size: 30rpx;border-radius: 40rpx;letter-spacing: 10rpx;}
</style>
