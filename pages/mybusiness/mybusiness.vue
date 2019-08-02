<template>
	<view class="container">
		<!-- header部分 -->
		<view class="header flex flexCenter">
			<view class="header_centerbox flex">
				<view class="num">15</view>
				<view style="width: 100%;height: 50rpx;"></view>
				<view class="unit">个</view>
			</view>
		</view>
		<view style="width: 100%;height: 30rpx;"></view>
		<!-- list部分 -->
		<view class="list">
			<view class="list_item" v-for="(item,index) in my_list" :key="index">
				<view class="list_item_info">
					<view style="width: 100%;height: 20rpx;"></view>
					<view class="list_item_left_info flex">
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="item_tit">账号 : </view>
						<view style="width: 60rpx;height: 100%;"></view>
						<view class="item_main">{{item.my_list_acount}}</view>
					</view>
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="list_item_left_info flex">
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="item_tit">名称 : </view>
						<view style="width: 60rpx;height: 100%;"></view>
						<view class="item_main">{{item.my_list_name}}</view>
					</view>
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="list_item_left_info flex">
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="item_tit">电话 : </view>
						<view style="width: 60rpx;height: 100%;"></view>
						<view class="item_main">{{item.my_list_tel}}</view>
					</view>
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="list_item_left_info flex">
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="item_tit"> 所属员工: </view>
						<view style="width: 60rpx;height: 100%;"></view>
						<view class="item_main">{{item.my_list_staff}}</view>
					</view>
					<view style="width: 100%;height: 40rpx;"></view>
				</view>
				<view style="width: 100%;height: 30rpx;"></view>
			</view>
			<view style="width: 100%;height: 30rpx;"></view>
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
						"my_list_acount":"15698563220",
						"my_list_name":"哆啦A梦",
						"my_list_tel":"15698563220",
						"my_list_staff":"张丹"
						
					},
					{
						"my_list_acount":"15698563220",
						"my_list_name":"哆啦A梦",
						"my_list_tel":"15698563220",
						"my_list_staff":"张丹"
						
					},
					{
						"my_list_acount":"15698563220",
						"my_list_name":"哆啦A梦",
						"my_list_tel":"15698563220",
						"my_list_staff":"张丹"
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
	.header{width: 100%;height: 400rpx;background: #FF566D;}
	.header_centerbox{text-align: center;align-items: flex-end;}
	.num{font-size: 120rpx;color: #FFFFFF;line-height: 120rpx;}
	.unit{font-size: 30rpx;color: #FFFFFF;line-height: 30rpx;}
	
	/* list部分 */
	.list{margin: 0 30rpx;}
	.list_item{margin: 0 30rpx;justify-content: space-between;border-bottom: solid 1px #EAEAEA;border-radius: 30rpx;}
	.list_item_name{font-size: 28rpx;color: #212121;line-height: 28rpx;}
	.list_item_time{font-size: 28rpx;color: #666666;line-height: 28rpx;}
	.list_item_info{width: 100%;background: #FFFFFF;}
	.list_item_left_info{width: 100%;}
	.my_red{color: red;}
</style>
