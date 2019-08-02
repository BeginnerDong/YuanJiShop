<template>
	<view style="container">
		<view style="width: 100%;height: 30rpx;"></view>
		<view v-for="(item,index) in shop" :key="index">
			<view class="item">
				<view style="width: 100%;height: 30rpx;"></view>
				<view class="shop_name">{{item.shop_name}}</view>
				<view style="width: 100%;height: 20rpx;"></view>
				<view class="flex shop_address">
					<view>地址 : </view>
					<view class="shop_addressinfo">{{item.shop_address}}</view>
				</view>
				<view style="width: 100%;height: 30rpx;"></view>
				<view class="flex">
					<view><image style="width: 24rpx;height: 24rpx;" :src="item.shop_icon"></image></view>
					<view style="width: 20rpx;height: 100%;"></view>
					<view class="shop_info">{{item.shop_info}}</view>
				</view>
				<view style="width: 100%;height: 30rpx;"></view>
			</view>
			<view style="width: 100%;height: 20rpx;"></view>
		</view>
	</view>
</template>

<script>

	export default {
		data() {
			return {
				webself:this,
				shop:[
					{
						shop_name:"门店名称门店名称",
						shop_address:"陕西省西安市高新区大都荟A座",
						shop_icon:"../../static/images/choose-icon1.png",
						shop_info:"默认门店"
					},
					{
						shop_name:"门店名称门店名称",
						shop_address:"陕西省西安市高新区大都荟A座",
						shop_icon:"../../static/images/choose-icon2.png",
						shop_info:"默认门店"
					},
					{
						shop_name:"门店名称门店名称",
						shop_address:"陕西省西安市高新区大都荟A座",
						shop_icon:"../../static/images/choose-icon2.png",
						shop_info:"默认门店"
					},
					{
						shop_name:"门店名称门店名称",
						shop_address:"陕西省西安市高新区大都荟A座",
						shop_icon:"../../static/images/choose-icon2.png",
						shop_info:"默认门店"
					},
					{
						shop_name:"门店名称门店名称",
						shop_address:"陕西省西安市高新区大都荟A座",
						shop_icon:"../../static/images/choose-icon2.png",
						shop_info:"默认门店"
					}
				]
			}
		},
		methods: {
			
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{background: #F5F5F5;}
	.item{padding: 0 30rpx;background: #FFFFFF;}
	.shop_name{font-size: 26rpx;color: #222222;line-height: 26rpx;}
	.shop_address{font-size: 24rpx;color: #222222;line-height: 24rpx;opacity: .8;}
	.shop_info{font-size: 20rpx;color: #222222;line-height: 20rpx;opacity: .6;}
	.shop_addressinfo{margin-left: 10rpx;}
</style>
