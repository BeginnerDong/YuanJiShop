<template>
	<view>
		<view style="width: 100%;height: 30rpx;"></view>
		<view class="container">
			<view class="container_box">
				<view class="container_box_item flex">
					<view class="container_box_item_tit">账号 : </view>
					<view class="container_box_item_acount">{{userData.login_name}}</view>
				</view>
				<view class="container_box_item flex">
					<view class="container_box_item_tit">密码 : </view>
					<view class="container_box_item_acount">{{userData.password}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				webself: this,
				userData:{},
				level:''
			}
		},
		onLoad() {
			const self = this;

			var options = self.$Utils.getHashParameters();
			self.level = options[0].level;
			self.$Utils.loadAll(['getUserData'], self);
		},

		methods: {


			getUserData() {
				const self = this;
				const postData = {
					
				};
				if(self.level=='agent'){
					postData.tokenFuncName = 'getAgentToken'
				}else if(self.level=='shop'){
					postData.tokenFuncName = 'getShopToken'
				}else{
					postData.tokenFuncName = 'getStaffToken'
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0]
					}
					console.log('res', res)
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},

		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");

	page {
		background: #F5F5F5;
		display: flex;
		justify-content: center;
	}

	.container {
		width: 690rpx;
	}

	.container_box {
		background: #FFFFFF;
		border-radius: 30rpx;
	}

	.container_box_item {
		padding: 40rpx 0 50rpx;
		font-size: 30rpx;
		color: #212121;
	}

	.container_box_item_tit {
		width: 20%;
		text-align: center;
	}

	.container_box_item_acount {
		width: 80%;
	}
</style>
