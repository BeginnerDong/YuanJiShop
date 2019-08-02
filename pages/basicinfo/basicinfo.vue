<template>
	<view>
		<view style="width: 100%;height: 30rpx;"></view>
		<view class="container">
			<view class="container_box">
				<view class="container_box_item flex">
					<view class="container_box_item_tit">账号 : </view>
					<view class="container_box_item_acount">15698563220</view>
				</view>
				<view class="container_box_item flex">
					<view class="container_box_item_tit">密码 : </view>
					<view class="container_box_item_acount">efefvedgvbe123456</view>
				</view>
			</view>
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
	page{background: #F5F5F5;display: flex;justify-content: center;}
	.container{width: 690rpx;}
	.container_box{background: #FFFFFF;border-radius: 30rpx;}
	.container_box_item{padding: 40rpx 0 50rpx;font-size: 30rpx;color: #212121;}
	.container_box_item_tit{width: 20%;text-align: center;}
	.container_box_item_acount{width: 80%;}
</style>
