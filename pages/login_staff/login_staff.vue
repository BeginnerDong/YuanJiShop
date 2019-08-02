<template>
	<view class="container">
		<view class="logo">
			<image style="" src="../../static/images/login-img.png"></image>
		</view>
		<view style="width: 100%;height: 50rpx;"></view>
		<view class="user_info">
			<view class="user_info_item flex">
				<view class="flex">
					<image class="login_icon"  src="../../static/images/login-icon1.png"></image>
				</view>
				<view><input class="login_txt" type="text" placeholder="请输入账号"></view>
			</view>
			<view class="user_info_item flex">
				<view class="flex">
					<image class="login_icon"  src="../../static/images/login-icon2.png"></image>
				</view>
				<view><input class="login_txt" type="text" placeholder="请输入您的密码"></view>
			</view>
		</view>
		<view style="width: 100%;height: 186rpx;"></view>
		<view class="confirm flex flexCenter">
			<view class="confirm_box" @click="webself.$Router.navigateTo({route:{path:'/pages/staffentrance/staffentrance'}})">登录</view>
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
	page{background: #FFFFFF;}
	.container{width: 100%;}
	.logo{width: 100%;height: 492rpx;}
	.logo>image{width: 100%;height: 100%;}
	.login_icon{width: 33rpx;height: 33rpx;padding:0 30rpx;}
	.user_info{padding: 0 30rpx;}
	.user_info_item{width: 600rpx;border-bottom: solid 1px #EAEAEA;padding: 80rpx 0 10rpx;}
	.login_txt{width: 550rpx;font-size: 26rpx;color: #666666;opacity: .7;}
	.confirm_box{width: 690rpx;height: 80rpx;background: #FF566D;color: #FFFFFF;text-align: center;line-height: 80rpx;font-size: 30rpx;border-radius: 40rpx;letter-spacing: 10rpx;}
</style>
