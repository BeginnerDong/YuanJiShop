<template>
	<view class="container">
		<view class="logo">
			<view style="width: 100%;height: 40rpx;"></view>
			<image style="width: 366rpx;height: 91rpx;" src="../../static/images/record-img1.png"></image>
			<view style="width: 100%;height: 46rpx;"></view>
		</view>
		<view class="content">
			<view :key="index" class="content_box" v-for="(item,index) in my_list">
				<view class="content_item">
					<view style="width: 100%;height: 19rpx;"></view>
					<view class="content_item_time">{{item.record_time}}</view>
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="content_item_main flex">
						<view>
							<image class="item_icon" :src="item.record_src"></image>
						</view>
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="content_item_main_right">
							<view>
								<view style="width: 100%;height: 20rpx;"></view>
								<span class="item_name">{{item.record_name}}</span>
							</view>
							<view class="item_info">{{item.record_info}}</view>
						</view>
					</view>
					<view style="width: 100%;height: 50rpx;"></view>
					<view class="content_item_footer flex flexCenter">
						<view class="flex">
							<view class="content_item_footer_box" @click="webself.$Router.navigateTo({route:{path:'/pages/changecredit/changecredit'}})">
								兑换积分
							</view>
							<view style="width: 40rpx;height: 100%;"></view>
							<view class="content_item_footer_box" @click="webself.$Router.navigateTo({route:{path:'/pages/confirmreceipt/confirmreceipt'}})">
								确认收货
							</view>
						</view>
					</view>
				</view>
				<view style="width: 100%;height: 30rpx;"></view>
			</view>
		</view>
	</view>
</template>

<script>
	
	export default {
		components: {

		},
		data() {
			return {
				webself:this,
				my_list: [
					{
						"record_time":"2019-05-20",
						"record_src":"../../static/images/record-img.png",
						"record_name":"穿衣熊60cm",
						"record_info":"商品价值=金币500/积分480"
					},
					{
						"record_time":"2019-05-20",
						"record_src":"../../static/images/record-img.png",
						"record_name":"穿衣熊60cm",
						"record_info":"商品价值=金币500/积分480"
					},
					{
						"record_time":"2019-05-20",
						"record_src":"../../static/images/record-img.png",
						"record_name":"穿衣熊60cm",
						"record_info":"商品价值=金币500/积分480"
					},
					{
						"record_time":"2019-05-20",
						"record_src":"../../static/images/record-img.png",
						"record_name":"穿衣熊60cm",
						"record_info":"商品价值=金币500/积分480"
					}
				]
			}
		},
	}
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	.container{height: 100%;flex-direction: column;}
	.logo{width:100%; text-align: center;}
	.content{padding: 0 30rpx;}
	.content_item{width: 630rpx;height: 340rpx;background: #e29a9a;border-radius: 30rpx;padding: 0 30rpx;}
	.content_item_time{font-size: 24rpx;line-height: 24rpx;color: #FFFFFF;}
	.content_item_main_right{height:140rpx;display:flex;flex-direction: column;justify-content: space-between;}
	.item_icon{width: 140rpx;height: 140rpx;}
	.item_name{font-size: 28rpx;color: #FFFFFF;line-height: 28rpx;}
	.item_info{font-size: 22rpx;color: #FFFFFF;line-height: 22rpx;}
	.content_item_footer_box{width: 140rpx;height: 50rpx;color: #FFFFFF;background: #09c15f;border-radius: 25rpx;text-align: center;line-height: 50rpx;font-size: 26rpx;}
</style>
