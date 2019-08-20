<template>
	<view>
		<image :src="mainData.url" style="position: absolute;top:20%;width: 55%;height: 35%;;left:22%"></image>
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
				webself:this,
				mainData:''
			}
		},
		
		onLoad() {		
			const self = this;
			
			var options = self.$Utils.getHashParameters();
			if(options[0].level){
				self.level = options[0].level
			}
			self.$Utils.loadAll(['getMainData'], self);			
		},
		
		methods: {
				
				getMainData() {
					const self = this;
					const postData = {};
					postData.tokenFuncName = 'getProjectToken';
					postData.param = 'http://www.yuanjishangcheng.com/wx/?parent_no=' + uni.getStorageSync(
							'user_no') + '#/pages/playgame/playgame',
					postData.ext = 'png';
					if(self.level&&self.level=='shop'){
						postData.tokenFuncName = 'getShopToken';
						postData.param = 'http://www.yuanjishangcheng.com/wx/?parent_no=' + uni.getStorageSync(
								'shopNo') + '#/pages/playgame/playgame',
						postData.ext = 'png';
					}
					const callback = (res) => {
						console.log(res);
						self.mainData = res.info;
						self.$Utils.finishFunc('getMainData');
					};
					self.$apis.getQrCommonCode(postData, callback);
				},
				
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
