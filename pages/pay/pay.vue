<template>
	<view class="container">
		<view style="width: 100%;height: 30rpx;"></view>
		<view class="container_box">
			<view style="width: 100%;height: 50rpx;"></view>
			<view class="container_title flex">
				<view class="mycoins">
					<image class="mycoins_icon clearfix" src="../../static/images/home-icon4.png"></image>
					<span class="mycoins_title">50</span>
				</view>
				<view class="flex mycoins_word">我的金币</view>
			</view>
			<view style="width: 100%;height: 29rpx;"></view>
			<view class="my_list">
				<view class="box" :key="index" v-for="(item,index) in my_list">
						<view class="my_list_box flex">
							<view class="my_info flex">
								<image class="my_icon" style="width: 193rpx;height: 118rpx;" src="../../static/images/top-icon1.png"></image>
								<span class="title">{{item.my_title}}</span>
							</view>
							<view class="my_icon_box flex">
								<image class="my_icon" style="width: 106rpx;height: 110rpx;" src="../../static/images/top-icon2.png"></image>
								<view class="my_icon_tit">
									{{item.my_money}}
								</view>
							</view>
						</view>
						<view style="width: 100%;height: 20rpx;"></view>
					</view>
			</view>
		</view>
		<view style="width: 100%;height: 30rpx;"></view>
	</view>
</template>

<script>
	
	export default {
		components: {
			
		},
		data() {
			return {
				webself:this,
				my_list:[
					{
						"my_money":"5元",
						"my_title":"50金币"
					},
					{
						"my_money":"8元",
						"my_title":"100金币"
					},
					{
						"my_money":"18元",
						"my_title":"200金币"
					},
					{
						"my_money":"46元",
						"my_title":"500金币"
					},
					{
						"my_money":"46元",
						"my_title":"500金币"
					},
					{
						"my_money":"46元",
						"my_title":"500金币"

					}
				],
			}
		},
		methods: {
			
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{display: flex;justify-content: center;align-items: center;}
	.container_box{width: 630rpx;background: #D35365;border-radius: 30rpx;padding: 0 30rpx;}
	.mycoins{width: 500rpx;height: 40rpx;background: #b84252;border-radius: 20rpx;position: relative;}
	.mycoins_icon{width: 31rpx;height: 31rpx;position: absolute;left: 10rpx;top: 5rpx;}
	.mycoins_title{color: #FFFFFF;padding-left: 58rpx;}
	.container_title{}
	.mycoins_word{flex: 1;justify-content: flex-end;color: #FFFFFF;}
	
	.list{width: 100%;padding-top: 100rpx;}
	.mytool{border-radius: 30rpx;}
	.my_list_box{background: #B84252;padding: 30rpx 25rpx;justify-content: space-between;}
	.title{margin-left: 20rpx;font-size: 26rpx;color: #FFFFFF;}
	.my_icon_box{position: relative;}
	.my_icon{justify-content: flex-end;}
	.my_icon_tit{position: absolute;text-align: center;width: 100%;color: #FFFFFF;}
</style>
