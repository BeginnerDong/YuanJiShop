<template>
	<view>
		<view class="container">
			<view class="container_item flex">
				<view class="container_item_left">持卡人：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入持卡人的姓名" v-model="submitData.card_name"/>
				</view>
			</view>
			<view class="container_item flex">
				<view class="container_item_left">手机号：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您银行卡绑定的手机号" v-model="submitData.card_phone"/>
				</view>
			</view>
			<view class="container_item flex">
				<view class="container_item_left">开户行：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您的银行卡的开户行" v-model="submitData.bank"/>
				</view>
			</view>
			<view class="container_item flex">
				<view class="container_item_left">银行卡号：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您的银行卡号" v-model="submitData.card_id"/>
				</view>
			</view>
		</view>
		<view style="width: 100%;height: 200rpx;"></view>
		<view class="confirm flex flexCenter" @click="submit">
			<view class="confirm_box">确定</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				webself: this,
				submitData: {
					card_name: '',
					card_phone: '',
					card_id: '',
					bank:''
				},
				userData: {}
			}
		},
		onLoad() {
			const self = this;

			var options = self.$Utils.getHashParameters();
			if(options[0].level){
				self.level = options[0].level
			}
			self.$Utils.loadAll(['getUserData'], self);
		},



		methods: {

			getUserData() {
				const self = this;
				const postData = {
					tokenFuncName: 'getAgentToken'
				};
				if (self.level && self.level == 'staff') {
					postData.tokenFuncName = 'getStaffToken';				
				} else if (self.level && self.level == 'shop') {
					postData.tokenFuncName = 'getShopToken';					
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0],
							self.submitData.card_name = self.userData.info.card_name,
							self.submitData.card_phone = self.userData.info.card_phone,
							self.submitData.card_id = self.userData.info.card_id,
							self.submitData.bank = self.userData.info.bank
					}
					console.log('res', res)
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},

			submit() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getAgentToken';
				postData.data = self.$Utils.cloneForm(self.submitData)
				if (self.level && self.level == 'staff') {
					postData.tokenFuncName = 'getStaffToken';					
				} else if (self.level && self.level == 'shop') {
					postData.tokenFuncName = 'getShopToken';				
				};
				if (self.$Utils.checkComplete(self.submitData)) {
					const callback = (res) => {
						if (res.solely_code == 100000) {
							self.$Utils.showToast('绑定成功', 'none');
							setTimeout(function() {
								uni.navigateBack({
									delta:1
								})
							}, 500);
							
						} else {
							self.$Utils.showToast(res.msg, 'none')
						}
					};

					self.$apis.userInfoUpdate(postData, callback);
				} else {
					self.$Utils.showToast('请补全信息', 'none')
				};
			},




		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{background: #FFFFFF;}
	.applyforjoining_title{height: 30rpx;justify-content: flex-end;color: #EE9CA7;padding: 0 30rpx;}
	
	.recipientinfo_label{width: 140rpx;height: 50rpx;border-radius: 25rpx;border: solid 1px #EE9CA7;text-align: center;line-height: 50rpx;box-sizing: border-box;}
	.recipientinfo_label_actived{background: #F8546B;border: none;color: #FFFFFF;}

	.container{margin: 0 30rpx;background: #FFFFFF;padding: 0 30rpx;}
	.container_item{border-bottom: solid 1px #EAEAEA;padding: 30rpx 0;}
	.container_item_left{width:24%;font-size: 28rpx;color: #666666;}
	.container_item_right{width: 100%;height: 70rpx;padding:0 30rpx;flex: 1;}
	.container_item_right>input{text-indent: 5%;width: 100%;height: 100%;font-size: 24rpx;line-height: 75rpx;}
	.confirm_box{width: 600rpx;height: 80rpx;background: #FF566D;color: #FFFFFF;text-align: center;line-height: 80rpx;font-size: 30rpx;border-radius: 40rpx;}
</style>

