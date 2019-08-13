<template>
	<view style="container">
		<view style="width: 100%;height: 30rpx;"></view>
		<view v-for="(item,index) in mainData" :key="index">
			<view class="item">
				<view style="width: 100%;height: 30rpx;"></view>
				<view class="shop_name">{{item.title}}</view>
				<view style="width: 100%;height: 20rpx;"></view>
				<view class="flex shop_address">
					<view>地址 : </view>
					<view class="shop_addressinfo">{{item.description}}</view>
				</view>
				<view style="width: 100%;height: 30rpx;"></view>
				<view class="flex" @click="choose(index)">
					<view>
						<image style="width: 24rpx;height: 24rpx;" :src="item.log.length>0?'../../static/images/choose-icon1.png':'../../static/images/choose-icon2.png'"></image>
					</view>
					<view style="width: 20rpx;height: 100%;"></view>
					<view class="shop_info">默认门店</view>
				</view>
				<view style="width: 100%;height: 30rpx;"></view>
			</view>
			<view style="width: 100%;height: 20rpx;"></view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				webself: this,
				mainData:[],
				
				defalutLog:[]
			}
		},
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			var options = self.$Utils.getHashParameters();
			self.$Utils.loadAll(['getMainData','getDefalutLog'], self);
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
			
			choose(index){
				const self= this;
				self.chooseIndex = index;
				if(self.defalutLog.length==0){
					self.logAdd()
				}else{
					self.logUpdate()
				}
			},
			
			logUpdate() {
				const self = this;
				const postData = {
					tokenFuncName:'getProjectToken',
					data:{
						relation_id:self.mainData[self.chooseIndex].id,
					},
					searchItem:{
						id:self.defalutLog.id
					}
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.solely_code==100000) {
						self.$Utils.showToast('选择成功','none');
						uni.navigateBack({
							delta:1
						})
					}else{
						self.$Utils.showToast(res.msg,'none');
					}
				};
				self.$apis.logUpdate(postData, callback);
			},
			
			logAdd() {
				const self = this;
				const postData = {
					tokenFuncName:'getProjectToken',
					data:{
						relation_id:self.mainData[self.chooseIndex].id,
						type:2
					}			
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.solely_code==100000) {
						self.$Utils.showToast('选择成功','none');
						uni.navigateBack({
							delta:1
						})
					}else{
						self.$Utils.showToast(res.msg,'none');
					}
				};
				self.$apis.logAdd(postData, callback);
			},
			
			getDefalutLog() {
				const self = this;
				const postData = {
					tokenFuncName:'getProjectToken',
					searchItem:{
						thirdapp_id:2,
						type:2
					}			
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.defalutLog = res.info.data[0]
					}
					console.log('res', res)
					self.$Utils.finishFunc('getDefalutLog');
				};
				self.$apis.logGet(postData, callback);
			},

			getMainData() {
				const self = this;
				const postData = {
					searchItem:{
						thirdapp_id:2
					}			
				};
				postData.getBefore = {
					article: {
						tableName: 'Label',
						searchItem: {
							title: ['=', ['自提门店']],
						},
						middleKey: 'menu_id',
						key: 'id',
						condition: 'in',
					},
				};
				postData.getAfter = {
					log: {
						token:uni.getStorageSync('user_token'),
						tableName: 'Log',
						searchItem: {
							status:1
						},
						middleKey: 'id',
						key: 'relation_id',
						condition: 'in',
					},
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)
					}
					console.log('res', res)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");

	page {
		background: #F5F5F5;
	}

	.item {
		padding: 0 30rpx;
		background: #FFFFFF;
	}

	.shop_name {
		font-size: 26rpx;
		color: #222222;
		line-height: 26rpx;
	}

	.shop_address {
		font-size: 24rpx;
		color: #222222;
		line-height: 24rpx;
		opacity: .8;
	}

	.shop_info {
		font-size: 20rpx;
		color: #222222;
		line-height: 20rpx;
		opacity: .6;
	}

	.shop_addressinfo {
		margin-left: 10rpx;
	}
</style>
