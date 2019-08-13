<template>
	<view class="container">
		<!-- header部分 -->
		<view class="header">
			<view class="pay" @click="webself.$Router.redirectTo({route:{path:'/pages/pay/pay'}})">
				<span class="pay_title">充值</span>
			</view>
			<view class="header_box flex flexCenter">
				<view class="header_centerbox">
					<view class="num">{{userData.info?userData.info.balance:''}}</view>
					<view style="width: 100%;height: 50rpx;"></view>
					<view class="unit">金币 (个)</view>
				</view>
			</view>
		</view>
		<!-- list部分 -->
		<view class="list">
			<view class="list_item flex" v-for="(item,index) in mainData" :key="index">
				<view class="list_item_left">
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="list_item_name">{{item.trade_info}}</view>
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="list_item_time">{{item.create_time}}</view>
					<view style="width: 100%;height: 30rpx;"></view>
				</view>
				<view  :class="item.count>0?'my_red':''" class="list_item_right">{{item.count}}</view>
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
				webself:this,
				mainData:[],
				userData:{},
			
			}
		},
		
		onLoad() {		
			const self = this;
			
			var options = self.$Utils.getHashParameters();	
			self.$Utils.loadAll(['getMainData','getUserData'], self);			
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
					tokenFuncName:'getProjectToken',
					searchItem:{
						thirdapp_id: 2,
						type:2
					}				
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)	
					}
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
	page{background: #F5F5F5;}
	/* header部分 */
	.header{width: 100%;height: 400rpx;background: #FF566D;flex-direction: column;position: relative;}
	.header_box{width: 100%;height: 100%;}
	.header_centerbox{text-align: center;}
	.num{font-size: 120rpx;color: #FFFFFF;line-height: 120rpx;}
	.unit{font-size: 28rpx;color: #FFFFFF;line-height: 28rpx;}
	
	/* list部分 */
	.list{background: #FFFFFF;}
	.list_item{margin: 0 30rpx;justify-content: space-between;border-bottom: solid 1px #EAEAEA;}
	.list_item_name{font-size: 28rpx;color: #212121;line-height: 28rpx;}
	.list_item_time{font-size: 28rpx;color: #666666;line-height: 28rpx;}
	.my_red{color: red;}
	.pay{position: absolute;right: 5%;top: 5%;}
	.pay_title{background: #FCCE08;color: #FFFFFF;padding: 3rpx 10rpx;border-radius: 20rpx;}
</style>
