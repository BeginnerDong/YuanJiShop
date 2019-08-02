<template>
	<view class="container flex">
		<!-- header部分 -->
		<view class="header">
			<view class="header_hook">
				<image src="../../static/images/home-icon.png" mode=""></image>
			</view>
			<view class="header_menu">
				<view class="header_menu_item flex flexCenter" @click="webself.$Router.navigateTo({route:{path:'/pages/freeprizedraw/freeprizedraw'}})">
					<image class="header_menu_img" src="../../static/images/home-icon3.png"></image>
					<span class="header_menu_name flex">免费抽奖</span>
				</view>
				<view style="width: 100%;height:40rpx;"></view>
				<view class="header_menu_item flex flexCenter" @click="webself.$Router.navigateTo({route:{path:'/pages/personage/personage'}})">
					<image class="header_menu_img" src="../../static/images/home-icon2.png"></image>
					<span class="header_menu_name flex">个人中心</span>
				</view>	
				<view style="width: 100%;height:40rpx;"></view>
				<view class="header_menu_item flex flexCenter" @click="webself.$Router.navigateTo({route:{path:'/pages/gamedescription/gamedescription'}})">
					<image class="header_menu_img" src="../../static/images/home-icon1.png"></image>
					<span class="header_menu_name flex">游戏说明</span>
				</view>	
			</view>
			<view class="bearbox clearfix">
				<view class="bear flex flexCenter">
					<view class="bearbox_item flex flexCenter">
						<image style="width: 160rpx;height: 188rpx;" src="../../static/images/home-img1.png"></image>
						<view class="bearbox_item_info">
							<span class="bear_item_name">毛绒熊</span>
						</view>
						<view class="bearbox_item_msg">
							<span class="bear_item_height">60cm</span>
						</view>
					</view>
					<view class="bearbox_item flex flexCenter">
						<image style="width: 146rpx;height: 197rpx;" src="../../static/images/home-img2.png"></image>
						<view class="bearbox_item_info">
							<span class="bear_item_name">穿衣熊</span>
						</view>
						<view class="bearbox_item_msg">
							<span class="bear_item_height">60cm</span>
						</view>
					</view>
					<view class="bearbox_item flex flexCenter">
						<image style="width: 141rpx;height: 198rpx;" src="../../static/images/home-img3.png"></image>
						<view class="bearbox_item_info">
							<span class="bear_item_name">iPhoneX</span>
						</view>
						<view class="bearbox_item_msg">
							<span class="bear_item_height">64G</span>
						</view>
					</view>
					<view class="bearbox_item flex flexCenter">
						<image style="width: 165rpx;height: 202rpx;" src="../../static/images/home-img4.png"></image>
						<view class="bearbox_item_info">
							<span class="bear_item_name">惊喜包</span>
						</view>
						<view class="bearbox_item_msg">
							<span class="bear_item_height">随机大奖</span>
						</view>
					</view>
				</view>
			</view>
		</view>
		<!-- footer部分 -->
		<view class="footer flex">
			<view class="recharge">
				<view style="width: 100%;height: 30rpx;"></view>
				<view class="recharge_box flex">
					<view class="recharge_box_info flex">
						<image class="recharge_logo" src="../../static/images/home-icon4.png"></image>
						<span class="recharge_txt">50</span>
					</view>
					<view class="recharge_msg flex"  @click="webself.$Router.navigateTo({route:{path:'/pages/pay/pay'}})">
						<span class="recharge_btn">充值</span>
						<image src="../../static/images/home-icon6.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="start flex flexCenter">
				<view class="start_box clearfix flex flexCenter">
					<image style="width: 186rpx;height: 190rpx;position: absolute;" src="../../static/images/home-icon5.png"></image>
					<view class="start_info">
						<view class="start_info_begin">开始</view>
						<view style="width: 100%;height: 16rpx;"></view>
						<view class="start_info_time">10币/一次</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		components: {
			
		},
		methods: {
			
		},
		data(){
			return{
				webself:this
			}
		}
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	.container{height: 100%;flex-direction: column;}
	/* header部分 */
	.header{width: 100%;height:950rpx;position: relative;}
	.header_hook{width: 100%;height: 250rpx;}
	.header_hook>image{width: 100%;height: 100%;}
	.bearbox{position: absolute;left: 0;bottom: 1%;width: 100%;}
	.bear{align-items: flex-end;}
	.bearbox_item{text-align: center;flex: 1;position: relative;}
	.header_menu{width:100rpx;height: 200rpx;position: absolute;right: 2%;top: 20%;}
	.header_menu_item{width: 100%;height: 100rpx;position: relative;}
	.header_menu_img{width: 106rpx;height: 110rpx;}
	.header_menu_name{position: absolute;z-index: 1;line-height:34rpx;font-size: 28rpx;color: #FFFFFF;flex-wrap: wrap;width: 70%;text-align: center;}
	.bear_item_name{color: #FFFFFF;font-size: 24rpx;line-height: 24rpx;}
	.bearbox_item_info{position: absolute;bottom: 12%;}
	.bearbox_item_msg{position: absolute;bottom: 0%;}
	.bear_item_height{color: #212121;font-size: 20rpx;line-height: 20rpx;}
	/* footer部分 */
	.footer{width:100%;height: 300rpx;background:linear-gradient(#ff8190,#ee9ca7);padding: 0 30rpx;flex-direction: column;}
	.recharge_box_info{width: 520rpx;height: 40rpx;line-height:40rpx;background: #5A3932;border-radius:40rpx;}
	.recharge_txt{position: relative;left: 10%;color: #FFFFFF;}
	.recharge_logo{width: 31rpx;height: 31rpx;position: absolute;left: 5%;}
	.recharge_msg{width: 120rpx;height: 60rpx;margin-left: 45rpx;position: relative;}
	.recharge_msg>image{width: 100%;height: 100%;}
	.recharge_btn{position: absolute;left: 0;top: 0;bottom: 0;right: 0;margin: auto;z-index: 1;text-align: center;line-height: 54rpx;font-size: 28rpx;color: #FFFFFF;}
	.start{flex: 1;}
	.start_box{width: 186rpx;height: 190rpx;}
	.start_info{position: absolute;}
	.start_info_begin{font-size: 60rpx;color: #FFFFFF;line-height: 60rpx;}
	.start_info_time{font-size: 26rpx;color: #FF556B;line-height: 26rpx;}
</style>
