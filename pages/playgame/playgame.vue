<template>
	<view class="container flex">
		<!-- header部分 -->
		<view class="header">
			<view class='springBj'></view>
			<view style="position: absolute;top: 0;width:100%;height: 100%;z-index:999">
				<view style="width:15px;margin: 0 auto; transition: all 1s;" :style="'height:'+ropeHeight+'%'">
					<image style="width: 100%;height: 100%;" src="../../static/images/rope.png" mode=""></image>
				</view>
				<view class="header_hook" style="text-align: center;" v-show="hockStatus=='open'">
					<image style="width: 75px;height: 46px;" src="../../static/images/hockopen.png" mode=""></image>
				</view>
				<view class="header_hook" style="text-align: center;" v-show="hockStatus=='close'&&!web_isReward">
					<image style="width: 75px;height: 46px;" src="../../static/images/hockclose.png" mode=""></image>
				</view>
				<view class="header_hook" style="text-align: center;" v-show="hockStatus=='close'&&web_isReward">
					<image style="width: 160rpx;height: 188rpx;" src="http://106.12.155.217/yjsc/public/uploads/2/20190809/ab1094859169c39eb34cbf15071bbb6aid5.png"
					 mode=""></image>
				</view>
			</view>

			<view class="header_menu">
				<view class="header_menu_item flex flexCenter" @click="webself.$Router.navigateTo({route:{path:'/pages/freeprizedraw/freeprizedraw'}})">
					<image class="header_menu_img" src="../../static/images/home-icon3.png"></image>
					<span class="header_menu_name flex">免费抽奖</span>
				</view>
				<view style="width: 100%;height:40rpx;"></view>
				<view class="header_menu_item flex flexCenter" @click="webself.$Router.navigateTo({route:{path:'/pages/personage/personage'}})">
					<image class="header_menu_img" src="../../static/images/home-icon2.png"></image>
					<span class="header_menu_name flex">个人中心</span>
				</view>

			</view>
			<view class="header_menu" style="left: 2%;">
				<view class="header_menu_item flex flexCenter" @click="webself.$Router.navigateTo({route:{path:'/pages/productsexchange/productsexchange'}})">
					<image class="header_menu_img" src="../../static/images/home-icon7.png"></image>
					<span class="header_menu_name flex">兑换商城</span>
				</view>

				<view style="width: 100%;height:40rpx;"></view>
				<view class="header_menu_item flex flexCenter" @click="webself.$Router.navigateTo({route:{path:'/pages/gamedescription/gamedescription'}})">
					<image class="header_menu_img" src="../../static/images/home-icon1.png"></image>
					<span class="header_menu_name flex">游戏说明</span>
				</view>
			</view>

			<view class="bearbox clearfix">
				<!-- <scroll-view class="scroll-view_H" scroll-x="true" @scroll="scroll" >
                   <view id="demo1" class="scroll-view-item_H uni-bg-red">A</view>
                    <view id="demo2" class="scroll-view-item_H uni-bg-green">B</view>
                    <view id="demo3" class="scroll-view-item_H uni-bg-blue">C</view>
                </scroll-view>
					<view class="bear flex" v-if="status=='none'">
						<view class="bearbox_item flex scroll-view-item_H" v-for="item in mainData" >
							<image style="width: 160rpx;height: 188rpx;" :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''"></image>
							<view class="bear-cont">
								<view class="item_name overflow1">{{item.title}}</view>
								<view class="item_msg">{{item.description}}</view>
							</view>
							<view class="bearbox_item_info">
								<span class="bear_item_name">{{item.title}}</span>
							</view>
							<view class="bearbox_item_msg">
								<span class="bear_item_height">{{item.description}}</span>
							</view>
						</view>
					</view>
				</scroll-view> -->

				<view style="position: relative;width: 100%;height: 150px;">
					<view class="anim" style="position: absolute;top: 0;left: 0;width: 33.3%;text-align: center;" v-for="(item,index) in mainData"
					 :key="index">
						<image style="width: 160rpx;height: 188rpx;" :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''"></image>
						<view class="item_name overflow1">{{item.title}}{{index}}</view>
						<view class="item_msg">{{item.description}}</view>
					</view>
				</view>
			</view>
		</view>
		<!-- footer部分 -->
		<view class="footer flex" style="position: relative;">
			<view class="recharge">
				<view style="width: 100%;height: 30rpx;"></view>
				<view class="recharge_box flex">
					<view class="recharge_box_info flex">
						<image class="recharge_logo" src="../../static/images/home-icon4.png"></image>
						<span class="recharge_txt">{{userData.info?userData.info.balance:''}}</span>
					</view>
					<view class="recharge_msg flex" @click="webself.$Router.navigateTo({route:{path:'/pages/pay/pay'}})">
						<span class="recharge_btn">充值</span>
						<image src="../../static/images/home-icon6.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="start flex flexCenter">
				<view class="start_box clearfix flex flexCenter">
					<image style="width: 186rpx;height: 190rpx;position: absolute;" src="../../static/images/home-icon5.png"></image>
					<view class="start_info" @click="draw">
						<view class="start_info_begin" style="font-family:'剪纸简体'">
							<!-- {{status=='ready'?'抓':'开始'}} -->
							<image :src="status=='ready'?'../../static/images/star2.png':'../../static/images/star1.png' " style="width: 110rpx; height:53rpx; margin: 0 auto;"></image>
						</view>
						<view style="width: 100%;height: 8rpx;"></view>
						<view class="start_info_time">{{status=='ready'?timerCount+'s':'10币/一次'}}</view>
					</view>
				</view>
			</view>
			<image @click="radioClick()" :src="play?'../../static/images/musicOn.png':'../../static/images/musicPause.png'"
			 style="position: absolute;bottom: 20rpx;right: 20rpx;width: 40rpx;height: 40rpx;"></image>
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
				mainData: [],
				userData: {},
				status: 'none',
				newData: [],
				ropeHeight: 20,
				hockStatus: 'open',
				timerCount: 5,
				isReward: false,
				reward: {},
				web_isReward: false,
				play: false,
				startTime:0,
				totalLength:0
			}
		},

		onLoad() {
			const self = this;
			console.log(8888888);

			self.timestampNow = (new Date()).getTime();
			var options = self.$Utils.getHashParameters();

			/* if (options[0].parent_no) {
				var res = self.$Token.getProjectToken(function() {
					self.$Utils.loadAll(['getMainData', 'getLabelData'], self)
				}, {
					parent_no: options[0].parent_no
				});
				if (res) {
					self.$Utils.loadAll(['getMainData', 'getLabelData'], self)
				};
			} else {
				self.$Utils.loadAll(['getMainData', 'getLabelData'], self);
			} */

			self.$Utils.loadAll(['getMainData','tokenGet'], self);				
		},

		onShow() {
			const self = this;
			self.getUserData();

		},


		methods: {

			tokenGet() {
				const self = this;
				const postData = {
					searchItem: {
						user_no: 'U111111'
					}
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.solely_code == 100000) {
						uni.setStorageSync('user_token', res.token);
						uni.setStorageSync('user_no', res.info.user_no);
						uni.setStorageSync('user_info', res.info);
						uni.setStorageSync('token_expire_time', 1565505988000)
					}
					console.log('res', res)
					self.$Utils.finishFunc('tokenGet');
				};
				self.$apis.tokenGet(postData, callback);
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

				};
				self.$apis.userGet(postData, callback);
			},

			getLabelData() {
				const self = this;
				const postData = {
					searchItem: {
						title: '首页音乐'
					}
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.labelData = res.info.data[0]
						self.innerAudioContext = null;
						self.innerAudioContext = uni.createInnerAudioContext();
						console.log('innerAudioContext', self.innerAudioContext)
						self.innerAudioContext.autoplay = true;
						self.innerAudioContext.loop = true;
						self.innerAudioContext.src = self.labelData.mainImg[0].url;
						document.addEventListener('WeixinJSBridgeReady', function () {
						      self.innerAudioContext.play();
							  self.play=true
						 }, false)

						/* self.innerAudioContext.onPlay(() => {
						  console.log('开始播放');
						});
						self.innerAudioContext.onError((res) => {
						  console.log(res.errMsg);
						  console.log(res.errCode);
						}); */
					}
					self.$Utils.finishFunc('getLabelData');
				};
				self.$apis.labelGet(postData, callback);
			},

			radioClick() {
				const self = this;
				if (self.play) {
					self.innerAudioContext.pause();
					self.play = false
				} else {
					self.innerAudioContext.play();
					self.play = true
				}
			},

			getMainData() {
				const self = this;
				const postData = {
					searchItem: {
						thirdapp_id: 2,
						type: ['in', [3, 4]]
					}
				};

				console.log('postData', postData)
				const callback = (res) => {
					self.totalLength = res.info.data.length;
					if (res.info.data.length > 0) {
						if (res.info.data.length > 4) {
							var scrollCount = res.info.data.length - 4;
						} else {
							var scrollCount = 0;
						}

						const runkeyframes = "@keyframes aDirection {from {left: 0;}to {left: " + (scrollCount * 25 + 100) +
							"%;}} .anim {animation: aDirection " + (scrollCount * 0.7 + 2.8) +
							"s linear infinite;-webkit-animation: aDirection " + (scrollCount * 0.7 + 2.8) + "s linear infinite;}";
						console.log('runkeyframes', runkeyframes)
						// 创建style标签
						const style = document.createElement('style');
						// 设置style属性
						style.type = 'text/css';
						// 将 keyframes样式写入style内
						style.innerHTML = runkeyframes;
						// 将style样式存放到head标签
						console.log('document', document)
						document.getElementsByTagName('head')[0].appendChild(style);

						self.mainData.push(res.info.data[0]);
						self.startTime = (new Date()).getTime();
						//self.mainData.push.apply(self.mainData, res.info.data);
						for (var i = 1; i < res.info.data.length; i++) {
							(function(i) {
								setTimeout(function() {
									console.log('i', i)
									self.mainData.push(res.info.data[i]);
									console.log('self.mainData', self.mainData)
								}, i * 700);
							})(i)
						};
					}
					console.log('res', res)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.productGet(postData, callback);
			},

			draw() {
				const self = this;

				if (self.status == 'none') {
					if (parseFloat(self.userData.info.balance) < 10) {
						self.$Utils.showToast('您的金币不足', 'none');
						return
					};
					var oneTimeTime = self.totalLength * 700;
					var gapTime = (new Date()).getTime() + 1200 - self.startTime;
					console.log('oneTimeTime',oneTimeTime)
					if(gapTime>oneTimeTime){
						console.log('nb',((gapTime%oneTimeTime)/700).toFixed(2))
						var index =  Math.round(((gapTime%oneTimeTime)/700).toFixed(2));
					}else{
						console.log('(gapTime/700).toFixed(2)',(gapTime/700).toFixed(2))
						var index =  Math.round((gapTime/700).toFixed(2));
					};
					
					if(index>1){
						index = index - 1;
					}else{
						index = self.totalLength - 1;
					};

					console.log('gapTime',gapTime);
					console.log('index',index);
					const postData = {
						tokenFuncName: 'getProjectToken'
					};
					self.timerCount = 5;
					self.isReward = false;
					self.web_isReward = false;
					const callback = (res) => {
						self.status = 'ready';

						self.userData.info.balance = res.info.balance;
						if (res.info.product_no) {
							self.isReward = true;
							self.reward = res.info.productInfo;
						};
						self.newData.push({
							url: '../../static/images/gift.png',
						}, );
						self.interval = setTimeout(function() {
							self.newData.push({
								url: '../../static/images/gift.png',
							});
						}, 700);

						setTimeout(function() {
							self.newData.push({
								url: '../../static/images/gift.png',
							});
						}, 1900);

						setTimeout(function() {
							self.newData.push({
								url: '../../static/images/gift.png',
							});
						}, 2850);

						/* self.timeInterVal = setInterval(function() {
							if (self.timerCount > 0) {
								self.timerCount--;
							} else {
								clearInterval(self.timeInterVal);
								if (self.status == 'ready') {
									self.go()
								};
							};
						}, 1000) */
						//self.$Utils.showToast(res.msg,'none');
						console.log('res', res)
					};
					console.log('self.$apis.draw', self.$apis.draw);
					self.go()
					self.$apis.draw(postData, callback);
					return;
				};

				if (self.status == 'ready' && self.timerCount > 0) {
					self.go()
				};

			},

			go() {
				const self = this;
				self.ropeHeight = 70;
				self.status = 'go';
				setTimeout(function() {
					self.hockStatus = 'close';
					self.ropeHeight = 20;
					if (self.isReward) {
						self.web_isReward = true;
					};
					setTimeout(function() {
						if (self.isReward) {
							self.$Utils.showToast('恭喜！你的奖品：' + self.reward.title, 'none');
						} else {
							self.$Utils.showToast('下次好运', 'none');
						};
						self.hockStatus = 'open';
						self.status = 'none';
					}, 1200)
				}, 1200);
			}


		},


	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");

	.scroll-view-item_H {
		display: inline-block;
	}



	.springBj {
		width: 100%;
		height: 20%;
		position: absolute;
		top: 0rpx;
		left: 0;
		background: url(../../static/images/springBj.png) no-repeat center 0/100% 100%;
	}


	.bear-cont {
		width: 130rpx;
		height: 78rpx;
		border-radius: 10rpx;
		border: 2rpx solid #593932;
		background: #fff;
		position: absolute;
		box-sizing: border-box;
		overflow: hidden;
		text-align: center;
		bottom: -30rpx;
		left: 50%;
		transform: translateX(-50%);
	}

	.bear-cont .item_name {
		/* width: 100%; */
		line-height: 40rpx;
		background: #1e4dd3;
		font-size: 24rpx;
		color: #fff;
		padding: 0 6rpx;
		box-sizing: border-box;
	}

	.bear-cont .item_msg {
		line-height: 34rpx;
		background: #fff;
		font-size: 24rpx;
		padding: 0 6rpx;
		box-sizing: border-box;
	}

	.container {
		height: 100%;
		flex-direction: column;
	}

	/* header部分 */
	.header {
		width: 100%;
		height: 940rpx;
		position: relative;
	}

	.header_hook {
		width: 100%;
		height: 250rpx;
		z-index: 999999999;
	}

	.header_hook>image {
		width: 100%;
		height: 100%;
	}

	.bearbox {
		position: absolute;
		left: 0;
		bottom: 0;
		width: 100%;
		overflow: hidden;
	}

	.bear {
		align-items: flex-end;
		white-space: nowrap;
		padding: 0 30rpx 44rpx 30rpx;
		display: inline-block;
	}

	.bearbox_item {
		text-align: center;
		flex: 1;
		position: relative;
		margin: 0 10rpx;
	}

	.header_menu {
		width: 100rpx;
		position: absolute;
		right: 2%;
		top: 30%;
		z-index: 9999;
	}

	.header_menu_item {
		width: 100%;
		height: 100rpx;
		position: relative;
	}

	.header_menu_img {
		width: 106rpx;
		height: 110rpx;
	}

	.header_menu_name {
		position: absolute;
		z-index: 1;
		line-height: 34rpx;
		font-size: 28rpx;
		color: #FFFFFF;
		flex-wrap: wrap;
		width: 70%;
		text-align: center;
	}

	.bear_item_name {
		color: #FFFFFF;
		font-size: 24rpx;
		line-height: 24rpx;
	}

	.bearbox_item_info {
		position: absolute;
		bottom: 12%;
	}

	.bearbox_item_msg {
		position: absolute;
		bottom: 0%;
	}

	.bear_item_height {
		color: #212121;
		font-size: 20rpx;
		line-height: 20rpx;
	}

	/* footer部分 */
	.footer {
		width: 100%;
		height: 300rpx;
		background: linear-gradient(#ff8190, #ee9ca7);
		padding: 0 30rpx;
		flex-direction: column;
		box-sizing: border-box;
	}

	.recharge_box_info {
		width: 520rpx;
		height: 40rpx;
		line-height: 40rpx;
		background: #5A3932;
		border-radius: 40rpx;
	}

	.recharge_txt {
		position: relative;
		left: 10%;
		color: #FFFFFF;
	}

	.recharge_logo {
		width: 31rpx;
		height: 31rpx;
		position: absolute;
		left: 5%;
	}

	.recharge_msg {
		width: 120rpx;
		height: 60rpx;
		margin-left: 45rpx;
		position: relative;
	}

	.recharge_msg>image {
		width: 100%;
		height: 100%;
	}

	.recharge_btn {
		position: absolute;
		left: 0;
		top: 0;
		bottom: 0;
		right: 0;
		margin: auto;
		z-index: 1;
		text-align: center;
		line-height: 54rpx;
		font-size: 28rpx;
		color: #FFFFFF;
	}

	.start {
		flex: 1;
	}

	.start_box {
		width: 186rpx;
		height: 190rpx;
	}

	.start_info {
		position: absolute;
	}

	.start_info_begin {
		font-size: 60rpx;
		color: #FFFFFF;
		line-height: 60rpx;
	}

	.start_info_time {
		font-size: 26rpx;
		color: #FF556B;
		line-height: 26rpx;
		margin: 0 auto;
	}
</style>
