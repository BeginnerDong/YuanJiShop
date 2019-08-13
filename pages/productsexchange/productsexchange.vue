<template>
	<view class="container flex">
		<view class="item" v-for="(item,index) in mainData" :key="index" @click="webself.$Router.navigateTo({route:{path:'/pages/productdetails/productdetails?id='+item.id}})">
			<view class="item_icon">
				<image class="item_img" :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''"></image>
			</view>
			<view style="width: 100%;height: 30rpx;"></view>
			<view class="item_info">
				<view class="item_info_name">{{item.title}}</view>
				<view style="width: 100%;height: 20rpx;"></view>
				<view class="item_info_num">积分：<span>{{item.price}}</span></view>
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
				mainData:[]
			}
		},
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			var options = self.$Utils.getHashParameters();
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
			
					searchItem: {
						thirdapp_id: 2,
						type: 2
					},
					paginate: self.$Utils.cloneForm(self.paginate)
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data)
					}
					console.log('res', res)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.productGet(postData, callback);
			},
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");

	page {
		background: #F5F5F5;
	}

	.container {
		padding: 0 30rpx;
		flex-wrap: wrap;
	}

	.container .item:nth-child(odd) {
		margin-right: 30rpx;
	}

	.item {
		width: 330rpx;
		background: #FFFFFF;
		border-bottom-left-radius: 10rpx;
		border-bottom-right-radius: 10rpx;
		flex-direction: column;
		margin-top: 30rpx;
	}

	.item_icon {
		width: 330rpx;
		height: 256rpx;
	}

	.item_img {
		border-top-left-radius: 10rpx;
		border-top-right-radius: 10rpx;
	}

	.item_icon>image {
		width: 100%;
		height: 100%;
	}

	.item_info {
		padding: 0 20rpx;
	}

	.item_info_name {
		font-size: 28rpx;
		color: #222222;
		line-height: 28rpx;
	}

	.item_info_num {
		font-size: 28rpx;
		color: #FF3B3B;
		line-height: 28rpx;
	}
</style>
