<template>
	<view>
		<view class="footer">
			<view class="footer_box">
				<span class="notice">注：用户每天登陆或者推广其他用户均可以获取玩游戏次数</span>
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
			
		}
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{background:url(../../static/images/popularize.png) center top;background-size: cover;width: 100%;height: 100%;position: relative;}
	.footer{width: 100%;position: absolute;left: 0;bottom: 2%;}
	.footer_box{text-align: center;}
	.notice{font-size: 24rpx;color: #666666;line-height: 24rpx;}
</style>
