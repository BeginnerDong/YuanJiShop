<template>
	<view class="container">
		<view style="width: 100%;height: 40rpx;"></view>
		<view class="header">
			<image class="header_img" src="../../static/images/tules-icon1.png" mode=""></image>
			<view class="header_txt">
				<view class="header_info flex flexCenter">
					<view class="header_info_box">
						<view>1.玩法说明</view>
						<view style="width: 100%;height: 30rpx;"></view>
						<view>(1) 进入游戏后请小主们先关注游戏，每天登陆和分享都有机会有游戏币赠送哦~</view>
						<view>(2) 进入游戏后请小主们先关注游戏，每天登陆和分享都有机会有游戏币赠送哦~</view>
						<view>(3) 进入游戏后请小主们先关注游戏，每天登陆和分享都有机会有游戏币赠送哦~</view>
						<view>(4) 进入游戏后请小主们先关注游戏，每天登陆和分享都有机会有游戏币赠送哦~</view>
						<view>(5) 进入游戏后请小主们先关注游戏，每天登陆和分享都有机会有游戏币赠送哦~</view>
						<view>(6) 进入游戏后请小主们先关注游戏，每天登陆。</view>
					</view>
				</view>
			</view>
		</view>
		<view style="width: 100%;height: 40rpx;"></view>
		<view class="show">
			<image class="show_img_1" src="../../static/images/tules-img.png" mode=""></image>
			<image class="show_img_2" src="../../static/images/tules-img1.png" mode=""></image>
		</view>
		<view style="width: 100%;height: 40rpx;"></view>
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
	.header{position: relative;}
	.header_img{width: 100%;height: 900rpx;}
	.header_txt{}
	.header_info{position: absolute;width: 100%;left: 1%;top: 27%;}
	.header_info_box{width: 600rpx;height:480rpx;color: #70585c;overflow: hidden;font-size: 26rpx;}
	.show{padding: 0 30rpx;}
	.show_img_1{width: 100%;height: 825rpx;}
	.show_img_2{width: 100%;height: 1425rpx;}
</style>
