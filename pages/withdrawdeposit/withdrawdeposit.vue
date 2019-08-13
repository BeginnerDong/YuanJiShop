<template>
	<view class="container">
		<view style="width: 100%;height: 50rpx;"></view>
		<view class="container_header">
			<view class="container_header_box flex" @click="webself.$Router.navigateTo({route:{path:'/pages/cashaccount/cashaccount?level='+level}})">
				<view>去绑定银行卡</view>
				<view><image style="width: 12rpx;height: 22rpx;" src="../../static/images/about-icon8.png"></image></view>
			</view>
		</view>
		<view style="width: 100%;height: 150rpx;"></view>
		<view class="container_content">
			<view style="width: 100%;height: 50rpx;"></view>
			<view class="container_content_title">提现金额</view>
			<view style="width: 100%;height: 80rpx;"></view>
			<view class="container_content_num flex">
				<view class="icon_img">￥</view>
				<view class="icon_num"><input class="money_txt" type="number" v-model="submitData.count"></view>
			</view>
			<view style="width: 100%;height: 20rpx;"></view>
			<view class="container_content_explain flex">
				<view class="container_content_explain_left">本次可提现佣金{{userData.info?userData.info.balance:''}}元</view>
				<view class="alldeposit">全部提现</view>
			</view>
			<view style="width: 100%;height: 120rpx;" ></view>
				<view class="confirm flex flexCenter" @click="submit">
				<view class="confirm_box">提现</view>
			</view>
			<view style="width: 100%;height: 60rpx;"></view>
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
				userData:{},
				submitData:{
					count:''
				},
				level:''
			}
		},
		
		onLoad() {		
			const self = this;
			
			var options = self.$Utils.getHashParameters();
			if(options[0].level){
				self.level = options[0].level
			};
			self.$Utils.loadAll(['getUserData'], self);			
		},
		
		methods: {
			getUserData() {
				const self = this;
				const postData = {
					tokenFuncName:'getAgentToken'
				};
				if (self.level && self.level == 'staff') {
					postData.tokenFuncName = 'getStaffToken';			
				} else if (self.level && self.level == 'shop') {
					postData.tokenFuncName = 'getShopToken';		
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
			
			submit(){
				const self = this;
				if(self.userData.info.bank==''){
					self.$Utils.showToast('请绑定银行卡','none');				
				}else if(self.submitData.count==''){
					self.$Utils.showToast('请输入提现金额','none');
				}else if(self.submitData.count!=''&&parseInt(self.submitData.count)==0){
					self.$Utils.showToast('请输入正确金额','none');
				}else if(self.submitData.count!=''&&parseFloat(self.submitData.count)>parseFloat(self.userData.info.balance)){
					self.$Utils.showToast('余额不足','none');
				}else{
					self.flowLogAdd()
				}
			},
			
			flowLogAdd() {
				const self = this;
				const postData = {
					tokenFuncName:'getAgentToken',
					data:{
						count:self.submitData.count,
						trade_info:'提现',
						status:0,
						thirdapp_id:2,
						user_no:uni.getStorageSync('agentNo')
					}
				};
				if (self.level && self.level == 'staff') {
					postData.tokenFuncName = 'getStaffToken';	
					postData.data.user_no = uni.getStorageSync('staffNo')
				} else if (self.level && self.level == 'shop') {
					postData.tokenFuncName = 'getShopToken';	
					postData.data.user_no = uni.getStorageSync('shopNo')
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.solely_code==100000) {
						self.$Utils.showToast('申请成功','none');
						self.submitData.count = '';
						self.getUserData()
					}else{
						self.$Utils.showToast(res.msg,'none');
					}
				};
				self.$apis.flowLogAdd(postData, callback);
			}
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{background: #F5F5F5;}
	.container{padding: 0 30rpx;}
	.container_header_box{width: 630rpx;height: 100rpx;background: #FFFFFF;justify-content: space-between;padding: 0 30rpx;border-radius: 20rpx;}
	.container_content{width: 610rpx;height: 510rpx;background: #FFFFFF;padding: 0 40rpx;border-radius: 20rpx;}
	.container_content_title{font-size: 28rpx;color: #222222;line-height: 28rpx;}
	.icon_img{font-size: 60rpx;color: #222222;line-height: 60rpx;}
	.container_content_num{border-bottom: solid 1px #EAEAEA;}
	.icon_num{width: 100%;flex: 1;}
	.money_txt{width: 100%;}
	.container_content_explain{justify-content: space-between;font-size: 24rpx;line-height: 24rpx;}
	.container_content_explain_left{color: #222222;opacity: .6;}
	.alldeposit{color: #FF556B;}
	.confirm_box{width: 600rpx;height: 80rpx;background: #FF566D;color: #FFFFFF;text-align: center;line-height: 80rpx;font-size: 30rpx;border-radius: 40rpx;letter-spacing: 10rpx;}
</style>
