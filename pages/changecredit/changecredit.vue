<template>
	<view>
		<view style="width: 100rpx;height: 150rpx;"></view>
		<view class="container">
			<view class="container_title">兑换积分</view>
			<view style="width: 100%;height: 60rpx;"></view>
			<view class="container_num"><span class="container_title credit_des">
			{{mainData.product&&mainData.product[0]?mainData.product[0].score:''}}
			</span></view>
			<view style="width: 100%;height: 320rpx;"></view>
			<view class="confirm" @click="updateOrder">确定</view>
		</view>
	</view>
</template>

<script>
	export default {
		components: {

		},


		data() {
			return {
				webself: this,
				mainData:{},
				order_no:''
			}
		},

		onLoad() {
			const self = this;

			var options = self.$Utils.getHashParameters();
			if (options[0].order_no) {
				self.order_no = options[0].order_no
			};
			self.$Utils.loadAll(['getMainData'], self);
		},


		methods: {
			

			getMainData() {
				const self = this;
				const postData = {
					tokenFuncName: 'getProjectToken',
					searchItem: {
						thirdapp_id: 2,
						order_no: self.order_no
					},
				};
				postData.getAfter = {
					product: {
						
						tableName: 'Product',
						searchItem: {
							status: 1
						},
						middleKey: 'product_no',
						key: 'product_no',
						condition: 'in',
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
				self.$apis.orderGet(postData, callback);
			},
			
			updateOrder() {
				const self = this;
				const postData = {
					tokenFuncName: 'getProjectToken',
					searchItem: {
						thirdapp_id: 2,
						order_no: self.order_no
					},
					data:{
						reward_type:2,
						reward_status:1
					},
					saveAfter:[{
						tableName: 'FlowLog',
						FuncName: 'add',
						data: {
							user_no: uni.getStorageSync('user_no'),
							count: self.mainData.product[0].score,
							type:3,
							thirdapp_id:2,
							trade_info:'中奖兑换积分'
						}
					}]
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.solely_code==100000) {
						self.$Utils.showToast('兑换成功','none');
						setTimeout(function() {
							self.$Router.redirectTo({route:{path:'/pages/winningrecord/winningrecord'}})
						}, 500);
					}else{
						self.$Utils.showToast(res.msg,'none');
					}
					console.log('res', res)
					
				};
				self.$apis.orderUpdate(postData, callback);
			},


		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");

	.container {
		padding: 0 30rpx;
	}

	.container_title {
		font-size: 36rpx;
		color: #212121;
	}

	.container_num {
		border: solid 1px red;
		border-radius: 20rpx;
		width: 100%;
		height: 80rpx;
		line-height: 80rpx;
	}

	.container_num_box {}

	.credit_des {
		margin-left: 20rpx;
	}

	.confirm {
		width: 100%;
		height: 80rpx;
		line-height: 80rpx;
		text-align: center;
		background: #FF566D;
		border-radius: 20rpx;
		color: #FFFFFF;
		font-size: 36rpx;
		letter-spacing: 10rpx;
	}
</style>
