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
				<view><input class="login_txt" type="text" placeholder="请输入账号" v-model="submitData.login_name"></view>
			</view>
			<view class="user_info_item flex">
				<view class="flex">
					<image class="login_icon"  src="../../static/images/login-icon2.png"></image>
				</view>
				<view><input class="login_txt" type="password" placeholder="请输入您的密码" v-model="submitData.password"></view>
			</view>
		</view>
		<view style="width: 100%;height: 186rpx;"></view>
		<view class="confirm flex flexCenter">
			<view class="confirm_box" @click="submit">登录</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				webself:this,
				submitData:{
					login_name:'',
					password:''
				}
			}
		},
		
		onLoad(options) {
			const self = this;
			if (uni.getStorageSync('staffToken')) {
				uni.redirectTo({
					url: '/pages/staffentrance/staffentrance'
				})
			};
		},
		
		methods: {
			
			submit() {
				const self = this;
			
				const postData = {
					login_name: self.submitData.login_name,
					password:self.submitData.password
				};
				if (self.$Utils.checkComplete(self.submitData)) {
					
					const callback = (res) => {
						if (res.solely_code == 100000) {
							console.log(res);
							uni.setStorageSync('staffToken', res.token);
							uni.setStorageSync('staffNo', res.info.user_no);
							uni.setStorageSync('staffInfo', res.info);
							uni.redirectTo({
								url: '/pages/staffentrance/staffentrance'
							})
						} else {
							self.$Utils.showToast(res.msg,'none')
						}
					}
					self.$apis.staffLogin(postData, callback);
				} else {
					self.$Utils.showToast('请补全登录信息', 'none')
				};
			},
			
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
