<template>
	<view class="container">

		<view class="content">
			<view class="content_box flex flexCenter">
				<view style="width: 100%;height: 24rpx;"></view>
				<view class="content_item">
					<view style="width: 100%;height: 19rpx;"></view>
					<view class="content_item_time">{{mainData.create_time}}</view>
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="content_item_main flex">
						<view>
							<image class="item_icon" :src="mainData.mainImg&&mainData.mainImg[0]?mainData.mainImg[0].url:''"></image>
						</view>
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="content_item_main_right">
							<view>
								<view style="width: 100%;height: 20rpx;"></view>
								<span class="item_name">{{mainData.title}}</span>
							</view>
							<view class="item_info avoidOverflow">{{mainData.description}}</view>
						</view>
					</view>
					<view style="width: 100%;height: 50rpx;"></view>
				</view>
				<view style="width: 100%;height: 30rpx;"></view>
				<view class="recipientinfo">
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="recipientinfo_tit flex">
						<view class="recipientinfo_label " :class="type==1?'recipientinfo_label_actived':''" @click="changeType('1')">线上快递</view>
						<view style="width: 50rpx;height: 100%;"></view>
						<view class="recipientinfo_label" :class="type==2?'recipientinfo_label_actived':''" @click="changeType('2')">门店自营</view>
					</view>
					<view style="width: 100%;height: 50rpx;"></view>
					<view class="recipientinfo_info flex" v-if="type==1">
						<view class="flex">
							<image class="recipientinfo_info_icon" src="../../static/images/positioning-icon.png"></image>
							<view style="width: 30rpx;height: 100%;"></view>
							<view class="recipientinfo_info_msg" v-if="userData.info&&userData.info.address!=''">
								<view class="flex">
									<view class="recipientinfo_info_name item_name">{{userData.info?userData.info.name:''}}</view>

									<view class="recipientinfo_info_tel" style="margin-left: 20px;">{{userData.info?userData.info.phone:''}}</view>
								</view>
								<view style="width: 100%;height: 30rpx;"></view>
								<view class="recipientinfo_info_address">{{userData.info?userData.info.address:''}}</view>
							</view>
							<view class="recipientinfo_info_msg" v-if="userData.info&&userData.info.address==''">

								<view class="recipientinfo_info_address">请添加收货地址</view>
							</view>
						</view>
						<view @click="webself.$Router.navigateTo({route:{path:'/pages/receivingrecord/receivingrecord'}})">
							<image style="width: 12rpx;height: 22rpx;" src="../../static/images/about-icon8.png"></image>
						</view>
					</view>

					<view class="recipientinfo_info flex" v-if="type==2">
						<view class="flex">
							<image class="recipientinfo_info_icon" src="../../static/images/positioning-icon.png"></image>
							<view style="width: 30rpx;height: 100%;"></view>
							<view class="recipientinfo_info_msg" v-if="shopData.shop">
								<view class="flex">
									<view class="recipientinfo_info_name item_name">
										{{shopData.shop&&shopData.shop[0]?shopData.shop[0].title:''}}
									</view>
								</view>
								<view style="width: 100%;height: 30rpx;"></view>
								<view class="recipientinfo_info_address">地址：
									{{shopData.shop&&shopData.shop[0]?shopData.shop[0].description:''}}
								</view>
							</view>
							<view class="recipientinfo_info_msg" v-if="shopData.length==0">

								<view class="recipientinfo_info_address">请选择自提门店</view>
							</view>
						</view>
						<view @click="webself.$Router.navigateTo({route:{path:'/pages/tothestore/tothestore'}})">
							<image style="width: 12rpx;height: 22rpx;" src="../../static/images/about-icon8.png"></image>
						</view>
					</view>
				</view>
				<view style="width: 100%;height: 250rpx;"></view>
				<view class="confirm" @click="addOrder">确认</view>
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
				type: 1,
				webself: this,
				mainData: {},
				shopData: [],
				userData: {}
			}
		},

		onLoad() {
			const self = this;

			var options = self.$Utils.getHashParameters();
			if (options[0].id) {
				self.id = options[0].id
			}
		},

		onShow() {
			const self = this;
			self.$Utils.loadAll(['getMainData', 'getUserData', 'getShopData'], self);
		},

		methods: {
			changeType(type) {
				const self = this;
				if (self.type != type) {
					self.type = type
				}
			},

			getShopData() {
				const self = this;
				const postData = {
					tokenFuncName: 'getProjectToken',
					searchItem: {
						thirdapp_id: 2,
						type: 2
					}
				};
				postData.getAfter = {
					shop: {
						tableName: 'Article',
						searchItem: {
							status: 1
						},
						middleKey: 'relation_id',
						key: 'id',
						condition: 'in',
					},
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.shopData = res.info.data[0]
					}
					console.log('self.shopData', self.shopData)
					self.$Utils.finishFunc('getShopData');
				};
				self.$apis.logGet(postData, callback);
			},

			getUserData() {
				const self = this;
				const postData = {
					tokenFuncName: 'getProjectToken'
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

					searchItem: {
						thirdapp_id: 2,
						id: self.id
					},
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0]
					}
					console.log('res', res)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.productGet(postData, callback);
			},

			addOrder() {
				const self = this;
				var orderList = [];
				orderList.push({
					product: [{
						id: self.id,
						count: 1,
					}]
				})
				const postData = {
					tokenFuncName: 'getProjectToken',
					orderList: orderList,
					type: self.mainData.type,
					data:{}
					
				};
				if(self.type==1){
					if(self.userData.info.address==''){
						self.$Utils.showToast('请添加收货地址','none');
						return
					}else{
						postData.data.transport_type = 1;
						postData.snap_address = {
							name:self.userData.info.name,
							phone:self.userData.info.phone,
							address:self.userData.info.address
						}
					}
				}else if(self.type==2){
					if(self.shopData.length==0){
						self.$Utils.showToast('请选择自提门店','none');
						return
					}else{
						postData.data.transport_type = 2;
						postData.snap_shop = {
							title:self.shopData.shop[0].title,
							description:self.shopData.shop[0].description,
						}
					}
				}
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
				const postData = {
					score:parseFloat(price)
				};
				
				postData.tokenFuncName = 'getProjectToken',
				postData.searchItem = {
					id: self.orderId
				};
			
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
											setTimeout(function() {
												uni.navigateBack({
													delta:1
												})
											}, 1000);
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
								title: '支付成功',
								duration: 2000
							});
							setTimeout(function() {
								uni.navigateBack({
									delta:1
								})
							}, 1000);
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

	page {
		background: #F5F5F5;
	}

	.content {
		padding: 0 30rpx;
	}

	.content_box {
		flex-direction: column;
	}

	.content_item {
		width: 630rpx;
		height: 250rpx;
		background: #FFFFFF;
		border-radius: 30rpx;
		padding: 0 30rpx;
	}

	.content_item_time {
		font-size: 24rpx;
		line-height: 24rpx;
		color: #999999;
	}

	.content_item_main_right {
		height: 140rpx;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	.item_icon {
		width: 140rpx;
		height: 140rpx;
	}

	.item_name {
		font-size: 28rpx;
		color: #222222;
		line-height: 28rpx;
	}

	.item_info {
		font-size: 22rpx;
		color: #666666;
		line-height: 22rpx;
	}

	.recipientinfo {
		width: 630rpx;
		height: 261rpx;
		background: #FFFFFF;
		border-radius: 30rpx;
		padding: 0 30rpx;
	}

	.recipientinfo_tit {}

	.recipientinfo_label {
		width: 140rpx;
		height: 50rpx;
		border-radius: 25rpx;
		border: solid 1px #666666;
		text-align: center;
		line-height: 50rpx;
		box-sizing: border-box;
	}

	.recipientinfo_label_actived {
		background: #09C15F;
		border: none;
		color: #FFFFFF;
	}

	.recipientinfo_info {
		justify-content: space-between;
	}

	.recipientinfo_info_icon {
		width: 60rpx;
		height: 60rpx;
	}

	.recipientinfo_info_tel {
		font-size: 26rpx;
		color: #222222;
		line-height: 26rpx;
		opacity: .8;
	}

	.recipientinfo_info_name {}

	.recipientinfo_info_address {
		opacity: .9;
		font-size: 26rpx;
		color: #222222;
		line-height: 26rpx;
	}

	.confirm {
		width: 500rpx;
		height: 80rpx;
		background: #FF566D;
		color: #FFFFFF;
		text-align: center;
		line-height: 80rpx;
		font-size: 30rpx;
		border-radius: 40rpx;
	}
</style>
