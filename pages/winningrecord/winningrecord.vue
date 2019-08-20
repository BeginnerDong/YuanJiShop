<template>
	<view class="container">
		<view class="logo">
			<view style="width: 100%;height: 40rpx;"></view>
			<image style="width: 366rpx;height: 91rpx;" src="../../static/images/record-img1.png"></image>
			<view style="width: 100%;height: 46rpx;"></view>
		</view>
		<view class="content">
			<view :key="index" class="content_box" v-for="(item,index) in mainData">
				<view class="content_item">
					<view style="width: 100%;height: 19rpx;"></view>
					<view class="content_item_time">{{item.create_time}}</view>
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="content_item_main flex">
						<view>
							<image class="item_icon" 
							:src="item.product&&item.product[0]&&item.product[0].mainImg&&item.product[0].mainImg[0]?item.product[0].mainImg[0].url:''">
							</image>
						</view>
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="content_item_main_right">
							<view>
								<view style="width: 100%;height: 20rpx;"></view>
								<span class="item_name">{{item.product&&item.product[0]?item.product[0].title:''}}</span>
							</view>
							<view class="item_info">商品价值=金币{{item.product&&item.product[0]?item.product[0].price:''}}/积分{{item.product&&item.product[0]?item.product[0].score:''}}</view>
						</view>
					</view>
					<view style="width: 100%;height: 50rpx;"></view>
					<view class="content_item_footer flex flexCenter" style="padding-bottom: 20rpx;" v-if="item.reward_status==0">
						<view class="flex">
							<view class="content_item_footer_box" @click="webself.$Router.redirectTo({route:{path:'/pages/changecredit/changecredit?order_no='+item.order_no}})">
								兑换积分
							</view>
							<view style="width: 40rpx;height: 100%;"></view>
							<view class="content_item_footer_box" @click="webself.$Router.redirectTo({route:{path:'/pages/updateOrder/updateOrder?order_no='+item.order_no}})">
								确认收货
							</view>
						</view>
						
					</view>
					
				</view>
				<view style="width: 100%;height: 30rpx;"></view>
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
				webself: this,
				mainData:[],
				my_list: [{
						"record_time": "2019-05-20",
						"record_src": "../../static/images/record-img.png",
						"record_name": "穿衣熊60cm",
						"record_info": "商品价值=金币500/积分480"
					},
					{
						"record_time": "2019-05-20",
						"record_src": "../../static/images/record-img.png",
						"record_name": "穿衣熊60cm",
						"record_info": "商品价值=金币500/积分480"
					},
					{
						"record_time": "2019-05-20",
						"record_src": "../../static/images/record-img.png",
						"record_name": "穿衣熊60cm",
						"record_info": "商品价值=金币500/积分480"
					},
					{
						"record_time": "2019-05-20",
						"record_src": "../../static/images/record-img.png",
						"record_name": "穿衣熊60cm",
						"record_info": "商品价值=金币500/积分480"
					}
				]
			}
		},
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			var options = self.$Utils.getHashParameters();
			
		},
		
		onShow() {
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);
		},

		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},

		methods: {

			

			getMainData() {
				const self = this;
				const postData = {
					tokenFuncName:'getProjectToken', 
					searchItem: {
						thirdapp_id: 2,
						is_reward:1
					},
					paginate:self.$Utils.cloneForm(self.paginate)
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
						self.mainData.push.apply(self.mainData, res.info.data)
					}
					console.log('res', res)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
		},
	};
</script>


<style scoped>
	@import url("../../assets/style/public.css");

	.container {
		height: 100%;
		flex-direction: column;
	}

	.logo {
		width: 100%;
		text-align: center;
	}

	.content {
		padding: 0 30rpx;
	}

	.content_item {
		width: 630rpx;
		
		background: #e29a9a;
		border-radius: 30rpx;
		padding: 0 30rpx;
	}

	.content_item_time {
		font-size: 24rpx;
		line-height: 24rpx;
		color: #FFFFFF;
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
		color: #FFFFFF;
		line-height: 28rpx;
	}

	.item_info {
		font-size: 22rpx;
		color: #FFFFFF;
		line-height: 22rpx;
	}

	.content_item_footer_box {
		width: 140rpx;
		height: 50rpx;
		color: #FFFFFF;
		background: #09c15f;
		border-radius: 25rpx;
		text-align: center;
		line-height: 50rpx;
		font-size: 26rpx;
	}
</style>
