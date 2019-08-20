<template>
	<view>
		<view class="container flex">
			<view class="lotteryexplain flex" @click="webself.$Router.navigateTo({route:{path:'/pages/lotteryexplain/lotteryexplain'}})">
				<image style="width:30rpx;height: 30rpx;margin-right: 10rpx;" src="../../static/images/lucky-icon.png"></image>
				<span>抽奖说明</span>
			</view>
			<view class="giftbox flex flexCenter">
				<view class="gift">
					<image class="luky_gift" src="../../static/images/lucky-img1.png"></image>
				</view>
			</view>
			<view class="start flex flexCenter">
				<view class="start_box clearfix flex flexCenter" v-if="noProduct">
					<image style="width: 220rpx;height: 220rpx;position: absolute;" src="../../static/images/home-icon5.png"></image>
					<view class="start_info">
						<view class="start_info_begin">未开启</view>
					</view>
				</view>
				<view class="start_box clearfix flex flexCenter" v-if="!noProduct&&!hasOne"  @click="freeDraw">
					<image style="width: 220rpx;height: 220rpx;position: absolute;" src="../../static/images/home-icon5.png"></image>
					<view class="start_info">
						<view class="start_info_begin">参加</view>
					</view>
				</view>
				<view class="start_box clearfix flex flexCenter" v-if="!noProduct&&hasOne">
					<image style="width: 220rpx;height: 220rpx;position: absolute;" src="../../static/images/home-icon5.png"></image>
					<view class="start_info">
						<view class="start_info_begin">已参加</view>
					</view>
				</view>
			</view>
			<view style="width: 100%;height: 30rpx;"></view>
		</view>
		<view class="alertbox flex flexCenter" v-if="msg">
			<view class="alert">
				<view style="width: 100%;height: 20rpx;"></view>
				<view class="close flex">
					<img class="closeBtn" @click="closeAlert" src="../../static/images/del.png" alt="">
				</view>
				<view style="width: 100%;height: 40rpx;"></view>
				<view class="msg flex flexCenter">恭喜您中了穿衣熊的奖品</view>
				<view style="width: 100%;height: 80rpx;"></view>
				<view class="flex">
					<view class="select flex flexCenter">
						<view class="box yes" @click="closeAlert">确认</view>
					</view>					
				</view>
				<view style="width: 100%;height: 80rpx;"></view>
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
				msg:false,
				mainData:{},
				noProduct:true,
				hasOne:false
			}
		},
		
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			var options = self.$Utils.getHashParameters();
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			getMainData() {
				const self = this;
				const postData = {				
					searchItem: {
						thirdapp_id: 2,
						type:5,
						behavior:0
					},
					paginate:self.$Utils.cloneForm(self.paginate)
				};
				postData.order = {
					create_time:'asc'
				}
				postData.getAfter = {
					order: {	
						token:uni.getStorageSync('user_token'),
						tableName: 'Order',
						searchItem: {
							status: 1
						},
						middleKey: 'product_no',
						key: 'standard',
						condition: 'in',
					},
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						self.noProduct = false;
						if(res.info.data[0].order.length>0){
							self.hasOne = true
						};
					};
					console.log('res', res)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.productGet(postData, callback);
			},
			
			freeDraw() {
				const self = this;
				const postData = {	
					tokenFuncName:'getProjectToken',
					data:{
						product_no:self.mainData.product_no
					}
				};			
				console.log('postData', postData)
				const callback = (res) => {
					self.$Utils.showToast(res.msg,'none');
					console.log('res', res)
					setTimeout(function() {
						self.getMainData()
					}, 1000);
					
				};
				self.$apis.freeDraw(postData, callback);
			},
			
			
			
			showAlert(){
				this.msg = true;
			},
			closeAlert(){
				this.msg = false;
			}
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{background:linear-gradient(to bottom,#ffdde1,#ffafbd);position: relative;}
	.container{width: 100%;height:1240rpx;flex-direction: column;justify-content: space-between;}
	.lotteryexplain{position: absolute;top:2%;right: 5%;}
	.giftbox{flex: 1;}
	.gift{width: 433rpx;height: 544rpx;}
	.luky_gift{width: 100%;height: 100%;}
	.start{height: 190rpx;}
	.start_box{width: 186rpx;height: 190rpx;}
	.start_info{position: absolute;}
	.start_info_begin{font-size: 60rpx;color: #FFFFFF;line-height: 60rpx;}
	.start_info_time{font-size: 26rpx;color: #FF556B;line-height: 26rpx;}
	.alertbox{width: 100%;position: absolute;left: 0;top:0;bottom: 0;right: 0;margin: auto;}
	.alert{width: 630rpx;background: rgba(0,0,0,.4);padding: 0 30rpx;border-radius: 20rpx;}
	.msg{color: #FFFFFF;}
	.close{justify-content: flex-end;}
	.closeBtn{width: 34rpx;height: 34rpx;}
	.select{flex: 1;}
	.box{width: 120rpx;height: 50rpx;border-radius: 25rpx;text-align: center;line-height: 50rpx;color: #FFFFFF;}
	.yes{background: #FF526C;}
	.no{background: #E3E3E3;}
</style>
