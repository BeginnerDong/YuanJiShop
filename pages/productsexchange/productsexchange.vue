<template>
	<view class="container flex">
		<view class="item" v-for="(item,index) in my_list" :key="index" @click="webself.$Router.navigateTo({route:{path:'/pages/productdetails/productdetails'}})">
			<view class="item_icon">
				<image class="item_img" :src="item.my_list_src"></image>
			</view>
			<view style="width: 100%;height: 30rpx;"></view>
			<view class="item_info">
				<view class="item_info_name">{{item.my_list_name}}</view>
				<view style="width: 100%;height: 20rpx;"></view>
				<view class="item_info_num">积分：<span>{{item.my_list_num}}</span></view>
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
				my_list:[
					{
						"my_list_src":"../../static/images/imh1.png",
						"my_list_name":"大熊大熊大熊",
						"my_list_num":"56.55"
						
					},
					{
						"my_list_src":"../../static/images/imh1.png",
						"my_list_name":"大熊大熊大熊",
						"my_list_num":"56.55"
						
					},
					{
						"my_list_src":"../../static/images/imh1.png",
						"my_list_name":"大熊大熊大熊",
						"my_list_num":"56.55"
						
					},
					{
						"my_list_src":"../../static/images/comfirm.png",
						"my_list_name":"大熊大熊大熊",
						"my_list_num":"56.55"
						
					},
					{
						"my_list_src":"../../static/images/comfirm.png",
						"my_list_name":"大熊大熊大熊",
						"my_list_num":"56.55"
						
					},
					{
						"my_list_src":"../../static/images/comfirm.png",
						"my_list_name":"大熊大熊大熊",
						"my_list_num":"56.55"
						
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
	.container{padding: 0 30rpx;flex-wrap: wrap;}
	.container .item:nth-child(odd){margin-right: 30rpx;}
	.item{width: 330rpx;background: #FFFFFF;border-bottom-left-radius: 10rpx;border-bottom-right-radius: 10rpx;flex-direction: column;margin-top: 30rpx;}
	.item_icon{width: 330rpx;height: 256rpx;}
	.item_img{border-top-left-radius: 10rpx;border-top-right-radius: 10rpx;}
	.item_icon>image{width: 100%;height: 100%;}
	.item_info{padding: 0 20rpx;}
	.item_info_name{font-size: 28rpx;color: #222222;line-height: 28rpx;}
	.item_info_num{font-size: 28rpx;color: #FF3B3B;line-height: 28rpx;}
</style>
