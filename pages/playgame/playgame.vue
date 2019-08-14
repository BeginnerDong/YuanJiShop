<template>
	<view class="container flex">
		<!-- header部分 -->
		<view class="header">
			<view  style="width:15px;margin: 0 auto; transition: all 1s;" :style="'height:'+ropeHeight+'%'">
				<image style="width: 100%;height: 100%;" src="../../static/images/rope.png" mode=""></image>
			</view>
			<view class="header_hook" style="text-align: center;" v-show="hockStatus=='open'" >
				<image style="width: 75px;height: 46px;" src="../../static/images/hockopen.png" mode=""></image>
			</view>
			<view class="header_hook" style="text-align: center;" v-show="hockStatus=='close'&&!web_isReward" >
				<image style="width: 75px;height: 46px;" src="../../static/images/hockclose.png" mode=""></image>
			</view>
			<view class="header_hook" style="text-align: center;" v-show="hockStatus=='close'&&web_isReward" >
				<image style="width: 160rpx;height: 188rpx;" src="http://106.12.155.217/yjsc/public/uploads/2/20190809/ab1094859169c39eb34cbf15071bbb6aid5.png" mode=""></image>
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
				<view style="width: 100%;height:40rpx;"></view>
				<view class="header_menu_item flex flexCenter" @click="webself.$Router.navigateTo({route:{path:'/pages/gamedescription/gamedescription'}})">
					<image class="header_menu_img" src="../../static/images/home-icon1.png"></image>
					<span class="header_menu_name flex">游戏说明</span>
				</view>	
			</view>
			
			<view class="bearbox clearfix">
				<scroll-view>
					<view class="bear flex flexCenter" v-if="status=='none'">
						<view class="bearbox_item flex flexCenter " v-for="item in mainData">
							<image style="width: 160rpx;height: 188rpx;" :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''"></image>
							<view class="bearbox_item_info">
								<span class="bear_item_name">{{item.title}}</span>
							</view>
							<view class="bearbox_item_msg">
								<span class="bear_item_height">{{item.description}}</span>
							</view>
						</view>
					</view>
				</scroll-view>
				
				
				<view  style="position: relative;width: 100%;height: 100px;" v-if="status!='none'">
					<view class="anim" style="position: absolute;top: 0;left: 0;width: 33.3%;text-align: center;"  v-for="(item,index) in newData" :key="index">
						<image style="width: 160rpx;height: 188rpx;" :src="item.url"></image>	
					</view>
				
				</view>
			</view>
		</view>
		<!-- footer部分 -->
		<view class="footer flex">
			<view class="recharge">
				<view style="width: 100%;height: 30rpx;"></view>
				<view class="recharge_box flex">
					<view class="recharge_box_info flex">
						<image class="recharge_logo" src="../../static/images/home-icon4.png"></image>
						<span class="recharge_txt">{{userData.info?userData.info.balance:''}}</span>
					</view>
					<view class="recharge_msg flex"  @click="webself.$Router.navigateTo({route:{path:'/pages/pay/pay'}})">
						<span class="recharge_btn">充值</span>
						<image src="../../static/images/home-icon6.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="start flex flexCenter">
				<view class="start_box clearfix flex flexCenter">
					<image style="width: 186rpx;height: 190rpx;position: absolute;" src="../../static/images/home-icon5.png"></image>
					<view class="start_info" @click="draw">
						<view class="start_info_begin">{{status=='ready'?'抓':'开始'}}</view>
						<view style="width: 100%;height: 16rpx;"></view>
						<view class="start_info_time">{{status=='ready'?timerCount+'s':'10币/一次'}}</view>
					</view>
				</view>
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
				status:'none',
				newData:[],
				ropeHeight:10,
				hockStatus:'open',
				timerCount:5,
				isReward:false,
				reward:{},
				web_isReward:false
			}
		},
		
		onLoad() {		
			const self = this;
			console.log(8888888);
			
			self.timestampNow = (new Date()).getTime();
			var options = self.$Utils.getHashParameters();	
			self.$Utils.loadAll(['tokenGet'], self);			
			//self.$Utils.loadAll(['getMainData'], self);			
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
						uni.setStorageSync('token_expire_time',1565505988000)
					}
					console.log('res', res)
					self.getUserData();
					self.getMainData()
				};
				self.$apis.tokenGet(postData, callback);
			},
			
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
					self.$Utils.finishFunc('tokenGet');
				};
				self.$apis.userGet(postData, callback);
			},
			
			getMainData() {
				const self = this;
				const postData = {
					searchItem:{
						thirdapp_id: 2,
						type:['in',[3,4]]
					}				
				};
				
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)	
					}
					console.log('res', res)
					self.$Utils.finishFunc('getMainData');
					self.$Utils.finishFunc('tokenGet');
				};
				self.$apis.productGet(postData, callback);
			},
			
			draw() {
				const self = this;
				if(self.status=='none'){
					const postData = {
						tokenFuncName:'getProjectToken'
					};			
					self.timerCount = 5;
					self.isReward = false;
					self.web_isReward = false;
					const callback = (res) => {
						self.status = 'ready';
						self.userData.info.balance = res.info.balance;
						if(res.info.product_no){
							self.isReward = true;
							self.reward = res.info.productInfo;
						};
						self.newData.push({
							url:'../../static/images/gift.png',
						},);
						self.interval = setTimeout(function(){
							self.newData.push({
								url:'../../static/images/gift.png',
							});
						},950);
						
						setTimeout(function(){
							self.newData.push({
								url:'../../static/images/gift.png',
							});
						},1900);
						
						setTimeout(function(){
							self.newData.push({
								url:'../../static/images/gift.png',
							});
						},2850);
						
						self.timeInterVal =  setInterval(function(){
							if(self.timerCount>0){
								self.timerCount--;
							}else{
								clearInterval(self.timeInterVal);
								if(self.status=='ready'){
									self.go()
								};
							};
						},1000)
						//self.$Utils.showToast(res.msg,'none');
						console.log('res', res)
					};
					console.log('self.$apis.draw', self.$apis.draw);
					self.$apis.draw(postData, callback);
					return;
				};

				if(self.status=='ready'&&self.timerCount>0){
					self.go()
				};
				
			},
			
			go(){
				const self = this;
				self.ropeHeight = 80;
				self.status = 'go';
				setTimeout(function(){
					self.hockStatus = 'close';
					self.ropeHeight = 10;
					if(self.isReward){
						self.web_isReward =true;
					};
					setTimeout(function(){
						if(self.isReward){
							self.$Utils.showToast('恭喜！你的奖品：' + self.reward.title,'none');
						}else{
							self.$Utils.showToast('下次好运','none');
						};
						self.hockStatus = 'open';
						self.status = 'none';
					},1200)
				},1200);
			}
			
			
		},
		
		
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	.anim{
	
		animation:aDirection 3.8s linear infinite;
		-webkit-animation:aDirection 3.8s linear infinite;
	}
	@keyframes aDirection {
	    from {left:0;}
	    to {left:133%;}
	}
	.container{height: 100%;flex-direction: column;}
	/* header部分 */
	.header{width: 100%;height:950rpx;position: relative;}
	.header_hook{width: 100%;height: 250rpx;}
	.header_hook>image{width: 100%;height: 100%;}
	.bearbox{position: absolute;left: 0;bottom: 1%;width: 100%;}
	.bear{align-items: flex-end;}
	.bearbox_item{text-align: center;flex: 1;position: relative;}
	.header_menu{width:100rpx;height: 200rpx;position: absolute;right: 2%;top: 20%;}
	.header_menu_item{width: 100%;height: 100rpx;position: relative;}
	.header_menu_img{width: 106rpx;height: 110rpx;}
	.header_menu_name{position: absolute;z-index: 1;line-height:34rpx;font-size: 28rpx;color: #FFFFFF;flex-wrap: wrap;width: 70%;text-align: center;}
	.bear_item_name{color: #FFFFFF;font-size: 24rpx;line-height: 24rpx;}
	.bearbox_item_info{position: absolute;bottom: 12%;}
	.bearbox_item_msg{position: absolute;bottom: 0%;}
	.bear_item_height{color: #212121;font-size: 20rpx;line-height: 20rpx;}
	/* footer部分 */
	.footer{width:100%;height: 300rpx;background:linear-gradient(#ff8190,#ee9ca7);padding: 0 30rpx;flex-direction: column;}
	.recharge_box_info{width: 520rpx;height: 40rpx;line-height:40rpx;background: #5A3932;border-radius:40rpx;}
	.recharge_txt{position: relative;left: 10%;color: #FFFFFF;}
	.recharge_logo{width: 31rpx;height: 31rpx;position: absolute;left: 5%;}
	.recharge_msg{width: 120rpx;height: 60rpx;margin-left: 45rpx;position: relative;}
	.recharge_msg>image{width: 100%;height: 100%;}
	.recharge_btn{position: absolute;left: 0;top: 0;bottom: 0;right: 0;margin: auto;z-index: 1;text-align: center;line-height: 54rpx;font-size: 28rpx;color: #FFFFFF;}
	.start{flex: 1;}
	.start_box{width: 186rpx;height: 190rpx;}
	.start_info{position: absolute;}
	.start_info_begin{font-size: 60rpx;color: #FFFFFF;line-height: 60rpx;}
	.start_info_time{font-size: 26rpx;color: #FF556B;line-height: 26rpx;}
</style>
