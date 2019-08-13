<template>
	<view class="container">
		<!-- header部分 -->
		<view class="header flex flexCenter">
			<view class="header_centerbox flex">
				<view class="num">{{total}}</view>
				<view style="width: 100%;height: 50rpx;"></view>
				<view class="unit">个</view>
			</view>
		</view>
		<view style="width: 100%;height: 30rpx;"></view>
		<!-- list部分 -->
		<view class="list">
			<view class="list_item" v-for="(item,index) in mainData" :key="index">
				<view class="list_item_info">
					<view style="width: 100%;height: 20rpx;"></view>
					<view class="list_item_left_info flex">
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="item_tit">账号 : </view>
						<view style="width: 60rpx;height: 100%;"></view>
						<view class="item_main">{{item.user&&item.user[0]?item.user[0].login_name:''}}</view>
					</view>
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="list_item_left_info flex">
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="item_tit">名称 : </view>
						<view style="width: 60rpx;height: 100%;"></view>
						<view class="item_main">{{item.user&&item.user[0]&&item.user[0].info?item.user[0].info.name:''}}</view>
					</view>
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="list_item_left_info flex">
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="item_tit">电话 : </view>
						<view style="width: 60rpx;height: 100%;"></view>
						<view class="item_main">{{item.user&&item.user[0]&&item.user[0].info?item.user[0].info.phone:''}}</view>
					</view>
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="list_item_left_info flex">
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="item_tit"> 所属员工: </view>
						<view style="width: 60rpx;height: 100%;"></view>
						<view class="item_main">111</view>
					</view>
					<view style="width: 100%;height: 40rpx;"></view>
				</view>
				<view style="width: 100%;height: 30rpx;"></view>
			</view>
			<view style="width: 100%;height: 30rpx;"></view>
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
				mainData:[],
				total:''
			}
		},
		
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			var options = self.$Utils.getHashParameters();
			console.log(options)
			if(options[0].level){
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
						parent_no:uni.getStorageSync('agentNo'),
						level: 1
					},
					paginate: self.$Utils.cloneForm(self.paginate),
					getAfter:{
						user:{
							tableName:'User',
							middleKey:'child_no',
							key:'user_no',
							condition:'=',
							searchItem:{
								status:1
							}
						}
					}
				};
				if(self.level&&self.level=='agent'){
					postData.searchItem.level=2
				}else if(self.level&&self.level=='staff'){
					postData.tokenFuncName = 'getStaffToken';
					postData.searchItem.parent_no=uni.getStorageSync('staffNo')
				}
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data)
						
					}
					self.total = res.info.total;
					console.log('res', res)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.distriGet(postData, callback);
			},
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{background: #F5F5F5;}
	/* header部分 */
	.header{width: 100%;height: 400rpx;background: #FF566D;}
	.header_centerbox{text-align: center;align-items: flex-end;}
	.num{font-size: 120rpx;color: #FFFFFF;line-height: 120rpx;}
	.unit{font-size: 30rpx;color: #FFFFFF;line-height: 30rpx;}
	
	/* list部分 */
	.list{margin: 0 30rpx;}
	.list_item{margin: 0 30rpx;justify-content: space-between;border-bottom: solid 1px #EAEAEA;border-radius: 30rpx;}
	.list_item_name{font-size: 28rpx;color: #212121;line-height: 28rpx;}
	.list_item_time{font-size: 28rpx;color: #666666;line-height: 28rpx;}
	.list_item_info{width: 100%;background: #FFFFFF;}
	.list_item_left_info{width: 100%;}
	.my_red{color: red;}
</style>
