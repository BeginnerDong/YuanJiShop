<template>
	<view class="container">
		<!-- header部分 -->
		<view class="header">
			<view class="pay" @click="webself.$Router.navigateTo({route:{path:'/pages/pay/pay'}})">
				<span class="pay_title">充值</span>
			</view>
			<view class="header_box flex flexCenter">
				<view class="header_centerbox">
					<view class="num">120</view>
					<view style="width: 100%;height: 50rpx;"></view>
					<view class="unit">金币 (个)</view>
				</view>
			</view>
		</view>
		<!-- list部分 -->
		<view class="list">
			<view class="list_item flex" v-for="(item,index) in my_list" :key="index">
				<view class="list_item_left">
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="list_item_name">{{item.my_list_name}}</view>
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="list_item_time">{{item.my_list_time}}</view>
					<view style="width: 100%;height: 30rpx;"></view>
				</view>
				<view  :style="item.my_red?'my_red':''" class="list_item_right">{{item.my_list_num}}</view>
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
						"my_list_name":"抓娃娃",
						"my_list_time":"2019-05-23",
						"my_list_num":"-10",
						"my_red":false
						
					},
					{
						"my_list_name":"抓娃娃",
						"my_list_time":"2019-05-23",
						"my_list_num":"-10",
						"my_red":false
					},
					{
						"my_list_name":"充值",
						"my_list_time":"2019-05-23",
						"my_list_num":"+100",
						"my_red":false
					},
					{
						"my_list_name":"签到",
						"my_list_time":"2019-05-23",
						"my_list_num":"+10",
						"my_red":true
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
	/* header部分 */
	.header{width: 100%;height: 400rpx;background: #FF566D;flex-direction: column;position: relative;}
	.header_box{width: 100%;height: 100%;}
	.header_centerbox{text-align: center;}
	.num{font-size: 120rpx;color: #FFFFFF;line-height: 120rpx;}
	.unit{font-size: 28rpx;color: #FFFFFF;line-height: 28rpx;}
	
	/* list部分 */
	.list{background: #FFFFFF;}
	.list_item{margin: 0 30rpx;justify-content: space-between;border-bottom: solid 1px #EAEAEA;}
	.list_item_name{font-size: 28rpx;color: #212121;line-height: 28rpx;}
	.list_item_time{font-size: 28rpx;color: #666666;line-height: 28rpx;}
	.my_red{color: red;}
	.pay{position: absolute;right: 5%;top: 5%;}
	.pay_title{background: #FCCE08;color: #FFFFFF;padding: 3rpx 10rpx;border-radius: 20rpx;}
</style>
