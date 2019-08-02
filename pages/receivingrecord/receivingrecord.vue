<template>
	<view>
		<view style="width: 100%;height: 40rpx;"></view>
		<view class="container">
			<view style="width: 100%;height: 80rpx;"></view>
			<view class="container_item flex">
				<view class="container_item_left">姓名：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您的姓名" />
				</view>
			</view>
			<view style="width: 100%;height: 80rpx;"></view>
			<view class="container_item flex">
				<view class="container_item_left">电话：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您的手机号" />
				</view>
			</view>
			<view style="width: 100%;height: 80rpx;"></view>
			<view class="container_item flex">
				<view class="container_item_left">地址：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您的地址" />
				</view>
			</view>
			<view style="width: 100%;height: 300rpx;"></view>
			<view class="confirm flex flexCenter">
				<view class="confirm_box">确定</view>
			</view>
			<view style="width: 100%;height: 80rpx;"></view>
		</view>
	</view>
</template>

<script>
	
	export default {
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
	.container{margin: 0 30rpx;background: #FFFFFF;}
	.container_item{justify-content: space-between;}
	.container_item_left{text-align: center;flex: 1;}
	.container_item_right{background: #F5F5F5;width: 555rpx;height: 70rpx;margin-right: 30rpx;}
	.container_item_right>input{text-indent: 5%;width: 100%;height: 100%;}
	.confirm_box{width: 600rpx;height: 80rpx;background: #FF566D;letter-spacing: 10rpx;color: #FFFFFF;text-align: center;line-height: 80rpx;font-size: 30rpx;border-radius: 40rpx;}
</style>

