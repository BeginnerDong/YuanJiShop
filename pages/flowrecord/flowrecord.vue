<template>
	<view class="container">
		<view class="flow_item clearfix flex flexCenter" v-for="(item,index) in mainData" :key="index">
			<view style="width: 100%;height: 30rpx;"></view>
			<view class="item flex">
				<view class="iteminfo flex">
					<view class="item_info_logo">
						<image class="my_icon" :src="item.user&&item.user[0]?item.user[0].headImgUrl:''"></image>
					</view>
					<view class="item_info_name">
						<view class="my_name"><span>{{item.user&&item.user[0]&&item.user[0].info?item.user[0].info.name:''}}</span></view>
						<view style="width: 100%;height: 30rpx;"></view>
						<view class="flex">
							<view>积分 ： </view>
							<view class="num">{{item.count}}</view>
						</view>
					</view>
				</view>
				<view class="flex">
					<span class="my_time">{{item.create_time}}</span>
					<view style="width: 30rpx;height: 100%;"></view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mainData:[],
				my_flow: [{
						flow_icon: "../../static/images/about-img.png",
						flow_name: "快乐的猫",
						flow_integral: 200,
						flow_time: "2019-05-30"
					},
					{
						flow_icon: "../../static/images/about-img.png",
						flow_name: "快乐的仔",
						flow_integral: 500,
						flow_time: "2019-05-30"
					},
					{
						flow_icon: "../../static/images/about-img.png",
						flow_name: "许你一世无忧",
						flow_integral: 800,
						flow_time: "2019-05-30"
					}
				]
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
						count:['>',0]
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
					}
				};
				if (self.level && self.level == 'staff') {
					postData.tokenFuncName = 'getStaffToken'
				} else if (self.level && self.level == 'shop') {
					postData.tokenFuncName = 'getShopToken'
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data)

					}
					self.total = res.info.total;
					console.log('res', res)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.flowLogGet(postData, callback);
			},
		},
	};
</script>

}
</script>

<style scoped>
	@import url("../../assets/style/public.css");

	page {
		background: #F5F5F5;
	}

	.item {
		width: 690rpx;
		height: 160rpx;
		background: #FFFFFF;
		border-radius: 30rpx;
		box-sizing: border-box;
		justify-content: space-between;
	}

	.flow_item {
		width: 100%;
		flex-direction: column;
	}

	.my_icon {
		width: 120rpx;
		height: 120rpx;
		border-radius: 50%;
		margin-left: 30rpx;
		margin-right: 20rpx;
	}

	.item_info {
		height: 100%;
		align-items: center;
	}

	.item_info_name {
		font-size: 26rpx;
		color: #212121;
	}

	.num {
		color: #FF556B;
	}

	.my_time {
		font-size: 24rpx;
		color: #666666;
	}
</style>
