<template>
	<view>
		<view class="container">
			<view class="container_item flex">
				<view class="container_item_left">持卡人：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入持卡人的姓名" />
				</view>
			</view>
			<view class="container_item flex">
				<view class="container_item_left">手机号：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您银行卡绑定的手机号" />
				</view>
			</view>
			<view class="container_item flex">
				<view class="container_item_left">开户行：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您的银行卡的开户行" />
				</view>
			</view>
			<view class="container_item flex">
				<view class="container_item_left">银行卡号：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您的银行卡号" />
				</view>
			</view>
		</view>
		<view style="width: 100%;height: 200rpx;"></view>
		<view class="confirm flex flexCenter" @click="webself.$Router.navigateTo({route:{path:'/pages/withdrawdeposit/withdrawdeposit'}})">
			<view class="confirm_box">确定</view>
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
	.applyforjoining_title{height: 30rpx;justify-content: flex-end;color: #EE9CA7;padding: 0 30rpx;}
	
	.recipientinfo_label{width: 140rpx;height: 50rpx;border-radius: 25rpx;border: solid 1px #EE9CA7;text-align: center;line-height: 50rpx;box-sizing: border-box;}
	.recipientinfo_label_actived{background: #F8546B;border: none;color: #FFFFFF;}

	.container{margin: 0 30rpx;background: #FFFFFF;padding: 0 30rpx;}
	.container_item{border-bottom: solid 1px #EAEAEA;padding: 30rpx 0;}
	.container_item_left{width:24%;font-size: 28rpx;color: #666666;}
	.container_item_right{width: 100%;height: 70rpx;padding:0 30rpx;flex: 1;}
	.container_item_right>input{text-indent: 5%;width: 100%;height: 100%;font-size: 24rpx;}
	.confirm_box{width: 600rpx;height: 80rpx;background: #FF566D;color: #FFFFFF;text-align: center;line-height: 80rpx;font-size: 30rpx;border-radius: 40rpx;}
</style>

