<template>
	<view class="container">
		<!-- header部分 -->
		<view class="header">
			<view class="header_img">
				<image style="width: 100%;height: 360rpx;" src="../../static/images/imh1.png"></image>
			</view>
			<view class="header_info">
				<view style="width: 100%;height: 30rpx;"></view>
				<view class="header_title">永生花永生花永生花</view>
				<view style="width: 100%;height: 30rpx;"></view>
				<view class="header_num">￥56.55</view>
				<view style="width: 100%;height: 30rpx;"></view>
				
			</view>
		</view>
		<view style="width: 100%;height: 20rpx;"></view>
		<view class="content">
			<view style="width: 100%;height: 30rpx;"></view>
			<view class="detail_title">商品详情</view>
			<view style="width: 100%;height: 20rpx;"></view>
			<view class="detail_main avoidOverflow4"><span>内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容。</span></view>
			<view style="width: 100%;height: 30rpx;"></view>
			<view class="flex flexCenter">
				<image class="content_img" src="../../static/images/imh1.png"></image>
			</view>
			<view style="width: 100%;height: 30rpx;"></view>
			<view class="detail_main avoidOverflow4"><span>内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容。</span></view>
			<view style="width: 100%;height: 30rpx;"></view>
			<view class="detail_main avoidOverflow4"><span>内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容。</span></view>
			<view style="width: 100%;height: 30rpx;"></view>
			<view class="detail_main avoidOverflow4"><span>内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容。</span></view>
			<view style="width: 100%;height: 80rpx;"></view>
		</view>
		<view class="change" @click="webself.$Router.navigateTo({route:{path:'/pages/confirmreceipt/confirmreceipt'}})">
			<view class="changeBtn">立即兑换</view>
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
	.header{background: #FFFFFF;}
	.header_info{padding: 0 30rpx;}
	.header_title{font-size: 30rpx;color: #222222;font-weight: bold;line-height: 30rpx;}
	.header_num{color: #FF3B3B;font-size: 30rpx;line-height: 30rpx;}
	.content{background: #FFFFFF;padding: 0 30rpx 94rpx;}
	.detail_title{font-size: 30rpx;color:#222222;line-height: 30rpx;}
	.detail_main{font-size: 28rpx;color: #666666;}
	.content_img{width: 600rpx;height: 340rpx;}
	.change{position: fixed;left: 0;bottom: 0;width: 100%;height: 94rpx;}
	.changeBtn{background: #FE556C;color: #FFFFFF;height: 94rpx;line-height: 94rpx;text-align: center;}
</style>
