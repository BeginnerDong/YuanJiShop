<template>
	<view class="container">
		<!-- header部分 -->
		<view class="header">
			<view class="pay" @click="webself.$Router.navigateTo({route:{path:'/pages/withdrawdeposit/withdrawdeposit?level='+level}})">
				<span class="pay_title">提现</span>
			</view>
			<view class="header_box flex flexCenter">
				<view class="header_centerbox">
					<view class="num">{{total}}</view>
					<view style="width: 100%;height: 50rpx;"></view>
					<view class="unit">佣金</view>
				</view>
			</view>
		</view>
		<!-- list部分 -->
		<view class="list">
			<view class="list_item flex" v-for="(item,index) in mainData" :key="index">
				<view class="list_item_left">
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="list_item_time">{{item.create_time}}</view>
					<view style="width: 100%;height: 30rpx;"></view>
				</view>
				<view :class="item.count>0?'my_red':''" class="list_item_right">{{item.count}}</view>
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
				total:'',
				webself: this,
				mainData:[],
				
			}
		},
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			var options = self.$Utils.getHashParameters();
			console.log(options)
			if (options[0].level) {
				self.level = options[0].level
			};
			console.log(self.level)
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



			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						pagesize: 5,
						is_page: true,
					}
				};
				const postData = {
					tokenFuncName: 'getAgentToken',
					searchItem: {
						type: 2,
						
					},
					paginate: self.$Utils.cloneForm(self.paginate),
					getAfter: {
						user: {
							tableName: 'User',
							middleKey: 'relation_user',
							key: 'user_no',
							condition: '=',
							searchItem: {
								status: 1
							}
						}
					},
					compute:{
					  totalCount:[
						'sum',
						'count',
						{type:2,user_no:uni.getStorageSync('agentNo')}
					  ]
					  
					}
				};
				if (self.level && self.level == 'staff') {
					postData.tokenFuncName = 'getStaffToken';
					postData.compute.totalCount[2].user_no = uni.getStorageSync('staffNo')
				} else if (self.level && self.level == 'shop') {
					postData.tokenFuncName = 'getShopToken';
					postData.compute.totalCount[2].user_no = uni.getStorageSync('shopNo')
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data)
					}
					self.total = res.info.compute.totalCount
					console.log('res', res)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.flowLogGet(postData, callback);
			},
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");

	page {
		background: #F5F5F5;
	}

	/* header部分 */
	.header {
		width: 100%;
		height: 400rpx;
		background: #FF566D;
		flex-direction: column;
		position: relative;
	}

	.header_box {
		width: 100%;
		height: 100%;
	}

	.header_centerbox {
		text-align: center;
	}

	.num {
		font-size: 120rpx;
		color: #FFFFFF;
		line-height: 120rpx;
	}

	.unit {
		font-size: 28rpx;
		color: #FFFFFF;
		line-height: 28rpx;
	}

	/* list部分 */
	.list {
		background: #FFFFFF;
	}

	.list_item {
		margin: 0 30rpx;
		justify-content: space-between;
		border-bottom: solid 1px #EAEAEA;
	}

	.list_item_name {
		font-size: 28rpx;
		color: #212121;
		line-height: 28rpx;
	}

	.list_item_time {
		font-size: 28rpx;
		color: #666666;
		line-height: 28rpx;
	}

	.my_red {
		color: red;
	}

	.pay {
		position: absolute;
		right: 5%;
		top: 5%;
	}

	.pay_title {
		background: #FCCE08;
		color: #FFFFFF;
		padding: 3rpx 10rpx;
		border-radius: 20rpx;
	}
</style>
