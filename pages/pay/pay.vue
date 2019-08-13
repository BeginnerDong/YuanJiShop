<template>
	<view class="container">
		<view style="width: 100%;height: 30rpx;"></view>
		<view class="container_box">
			<view style="width: 100%;height: 50rpx;"></view>
			<view class="container_title flex">
				<view class="mycoins">
					<image class="mycoins_icon clearfix" src="../../static/images/home-icon4.png"></image>
					<span class="mycoins_title">{{userData.info?userData.info.balance:''}}</span>
				</view>
				<view class="flex mycoins_word">我的金币</view>
			</view>
			<view style="width: 100%;height: 29rpx;"></view>
			<view class="my_list">
				<view class="box" :key="index" v-for="(item,index) in mainData">
						<view class="my_list_box flex">
							<view class="my_info flex">
								<image class="my_icon" style="width: 193rpx;height: 118rpx;" src="../../static/images/top-icon1.png"></image>
								<span class="title">{{item.score}}金币</span>
							</view>
							<view class="my_icon_box flex" @click="addOrder(index)">
								<image class="my_icon" style="width: 106rpx;height: 110rpx;" src="../../static/images/top-icon2.png"></image>
								<view class="my_icon_tit">
									{{item.price}}元
								</view>
							</view>
						</view>
						<view style="width: 100%;height: 20rpx;"></view>
					</view>
			</view>
		</view>
		<view style="width: 100%;height: 30rpx;"></view>
	</view>
</template>

<script>
	
	export default {
		components: {
			
		},
		data() {
			return {
				webself:this,
				mainData:[],
				userData:{}
			}
		},
		
		onLoad() {		
			const self = this;
			self.timestampNow = (new Date()).getTime();
			var options = self.$Utils.getHashParameters();	
			self.$Utils.loadAll(['getMainData','getUserData'], self);			
		},
		
		onReachBottom() {	
			const self = this;
			if (!self.isLoadAll&&uni.getStorageSync('canClick')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		methods: {
			
			getUserData() {
				const self = this;
				const postData = {
					tokenFuncName:'getProjectToken'
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
			
			getMainData() {
				const self = this;
				const postData = {
					searchItem:{
						thirdapp_id: 2,
						type:1
					}				
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)	
					}else {
						self.isLoadALL = true
					}
					console.log('res', res)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.productGet(postData, callback);
			},
			
			addOrder(index) {
				const self = this;	
				var orderList = [];
				orderList.push({
					product: [{
						id: self.mainData[index].id,
						count: 1,	
					}]
				})			
				const postData = {
					tokenFuncName: 'getProjectToken',
					orderList: orderList,
					type: self.mainData[index].type,
				};	
				const callback = (res) => {
			
					if (res && res.solely_code == 100000) {
						self.orderId = res.info.id;
						self.pay(self.orderId)
					} else {
					
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};
				};
				self.$apis.addOrder(postData, callback);
			},
			
			pay(order_id) {
				const self = this;
				var price = parseFloat(self.mainData.price);
				const postData = {};	
				postData.wxPay = {
					price: parseFloat(self.mainData.price)
				};
				postData.tokenFuncName = 'getProjectToken',
				postData.searchItem = {
					id: self.orderId
				};
				postData.payAfter = [];
				const callback = (res) => {
					if (res.solely_code == 100000) {
						if (res.info) {
							const payCallback = (payData) => {
								console.log('payData', payData)
								if (payData == 1) {
									uni.showToast({
										title: '支付成功',
										duration: 2000,
										success: function() {
											
										}
									});
								} else {
									
									uni.showToast({
										title: '支付失败',
										duration: 2000
									});
								};
							};
							self.$Utils.realPay(res.info, payCallback);
						} else {
							
							uni.showToast({
								title: '支付完成',
								duration: 2000
							});
						};
					} else {
						uni.setStorageSync('canClick', true);
						uni.showToast({
							title: '支付参数有误',
							duration: 2000
						});
					};
				};
				self.$apis.pay(postData, callback);
			},
			
			
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{display: flex;justify-content: center;align-items: center;}
	.container_box{width: 630rpx;background: #D35365;border-radius: 30rpx;padding: 0 30rpx;}
	.mycoins{width: 500rpx;height: 40rpx;background: #b84252;border-radius: 20rpx;position: relative;}
	.mycoins_icon{width: 31rpx;height: 31rpx;position: absolute;left: 10rpx;top: 5rpx;}
	.mycoins_title{color: #FFFFFF;padding-left: 58rpx;}
	.container_title{}
	.mycoins_word{flex: 1;justify-content: flex-end;color: #FFFFFF;}
	
	.list{width: 100%;padding-top: 100rpx;}
	.mytool{border-radius: 30rpx;}
	.my_list_box{background: #B84252;padding: 30rpx 25rpx;justify-content: space-between;}
	.title{margin-left: 20rpx;font-size: 26rpx;color: #FFFFFF;}
	.my_icon_box{position: relative;}
	.my_icon{justify-content: flex-end;}
	.my_icon_tit{position: absolute;text-align: center;width: 100%;color: #FFFFFF;}
</style>
