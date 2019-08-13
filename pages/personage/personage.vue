<template>
	<view>
		<view class="container">
			<!-- header部分 -->
			<view class="header">
				<view class="header_info clearfix flex flexCenter">
					<view class="mine flex">
						<view class="mine_info flex">
							<view class="mine_info_logo">
								<image class="my_icon" src="../../static/images/about-img.png"></image>
							</view>
							<view class="mine_info_name">
								<view class="my_name"><span>{{userData.nickname}}</span></view>
								<view style="width: 100%;height: 30rpx;"></view>
								<view class="my_degree" v-if="userData.info&&userData.info.balance>0">V会员</view>
							</view>
						</view>
						<view class="mine_playgame" @click="webself.$Router.redirectTo({route:{path:'/pages/playgame/playgame'}})">
							<span class="playgame_txt">玩游戏</span>
						</view>
					</view>
				</view>
				<view class="signIn">
					<view class="signIn_box flex">
						<view class="signIn_info flex" @click="signIn">
							<image style="width: 26rpx;height: 26rpx;margin-right: 10rpx;" src="../../static/images/about-icon7.png" mode=""></image>
							<span class="signIn_info_txt">{{userData.log&&userData.log.length>0?'已签到':'签到'}}</span>
						</view>
					</view>
				</view>
				<image style="width: 100%;height:215rpx;" src="../../static/images/about-img0.png"></image>
				
			</view>
			<!-- list部分 -->
			<view class="list">
				<view class="my_list">
					<view class="my_list_title flex">
						<view class="nav"></view>
						<view style="width: 20rpx;height: 100%;"></view>
						<span>我的工具</span>
					</view>
					<view class="mytool">
						<view class="box" :key="index" v-for="(item,index) in my_list" @click="goPage(item.my_key)">
							<view class="my_list_box flex">
								<view class="my_info flex" >
									<image style="width: 32rpx;height: 32rpx;" :src="item.my_src"></image>
									<span class="title">{{item.my_title}}</span>
								</view>
								<image class="my_icon" style="width: 10rpx;height: 20rpx;" src="../../static/images/about-icon8.png"></image>
							</view>
						</view>
					</view>
				</view>
				<view class="my_list">
					<view class="my_list_title flex">
						<view class="nav"></view>
						<view style="width: 20rpx;height: 100%;"></view>
						<span>第三方入口</span>
					</view>
					<view class="mytool">
						<view class="box" :key="index" v-for="(item,index) in my_enter" @click="goPage(item.my_key)">
							<view class="my_list_box flex">
								<view class="my_info flex" >
									<image style="width: 32rpx;height: 32rpx;" :src="item.my_src"></image>
									<span class="title">{{item.my_title}}</span>
								</view>
								<image class="my_icon" style="width: 10rpx;height: 20rpx;" src="../../static/images/about-icon8.png"></image>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		<!--浮窗-->
		<view class="mask" v-if="showView">
			<span class="sucess_text">恭喜获得{{reward}}金币~</span>
			<view class="alertFcBox flex flexCenter" v-if="showView">
				<img style="width: 602rpx;height: 403rpx;z-index:20 ;" src="../../static/images/success.png" alt="">
				<view>
					<img class="closeBtn" @click="closeAlert"  src="../../static/images/wrong-icon.png" alt="">
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import success from "../../components/success/success.vue"
	export default {
		components: {
			success
		},
		data() {
			return {
				userData:{},
				reward:'',
				showView: false,
				webself:this,
				my_list:[
					{
						"my_src":"../../static/images/about-icon1.png",
						"my_title":"我的积分",
						"my_key":"myintegral"
					},
					{
						"my_src":"../../static/images/about-icon2.png",
						"my_title":"我的金币",
						"my_key":"mycoins"
					},
					{
						"my_src":"../../static/images/about-icon3.png",
						"my_title":"中奖记录",
						"my_key":"winningrecord"
					},
					{
						"my_src":"../../static/images/about-icon4.png",
						"my_title":"收货记录",
						"my_key":"receivingrecord"
					},
					{
						"my_src":"../../static/images/about-icon5.png",
						"my_title":"推广海报",
						"my_key":"promotionposter"
					},
					{
						"my_src":"../../static/images/about-icon6.png",
						"my_title":"申请加盟",
						"my_key":"applyforjoining"
					}
				],
				my_enter:[
					{
						"my_src":"../../static/images/about-icon1.png",
						"my_title":"代理入口",
						"my_key":"login_agent"
					},
					{
						"my_src":"../../static/images/about-icon2.png",
						"my_title":"员工入口",
						"my_key":"login_staff"
					},
					{
						"my_src":"../../static/images/about-icon3.png",
						"my_title":"商家入口",
						"my_key":"login_merchant"
					}
				]
			}
		},
		
		onLoad() {		
			const self = this;
			self.reward  = uni.getStorageSync('user_info').thirdApp.custom_rule.sign;
			var options = self.$Utils.getHashParameters();	
			self.$Utils.loadAll(['getUserData'], self);			
		},
		
		
		methods: {
			goPage(id) {
				if(id=="myintegral"){
					this.$Router.navigateTo({route:{path:'/pages/myintegral/myintegral'}});
				}else if(id=="mycoins"){
					this.$Router.navigateTo({route:{path:'/pages/mycoins/mycoins'}});
				}else if(id=="winningrecord"){
					this.$Router.navigateTo({route:{path:'/pages/winningrecord/winningrecord'}});
				}else if(id=="receivingrecord"){
					this.$Router.navigateTo({route:{path:'/pages/receivingrecord/receivingrecord'}});
				}else if(id=="promotionposter"){
					this.$Router.navigateTo({route:{path:'/pages/promotionposter/promotionposter'}});
				}else if(id=="applyforjoining"){
					this.$Router.navigateTo({route:{path:'/pages/applyforjoining/applyforjoining'}});
				}else if(id=="login_agent"){
					this.$Router.navigateTo({route:{path:'/pages/login_agent/login_agent'}});
				}else if(id=="login_staff"){
					this.$Router.navigateTo({route:{path:'/pages/login_staff/login_staff'}});
				}else if(id=="login_merchant"){
					this.$Router.navigateTo({route:{path:'/pages/login_merchant/login_merchant'}});
				}
			},
			
			getUserData() {
				const self = this;
			
				const postData = {
					tokenFuncName:'getProjectToken'
				};
				postData.getAfter = {
					log:{
						tableName:'Log',
						middleKey:'user_no',
						key:'user_no',
						searchItem:{
							status:1,
							create_time:['between',[new Date(new Date().toLocaleDateString()).getTime()/1000,
							new Date(new Date().toLocaleDateString()).getTime() +24 * 60 * 60  -1]]
						},
						condition:'='
					}
				},
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
			
			signIn(){
				const self = this;
				
				if(self.userData.log.length>0){
					self.$Utils.showToast('今日已签到','none');
				}else{
					const postData = {
						tokenFuncName:'getProjectToken',
						data:{
							type:1
						},
						saveAfter:[{
							tableName: 'FlowLog',
							FuncName: 'add',
							data: {
								user_no: uni.getStorageSync('user_no'),
								count: self.reward,
								type:2,
								thirdapp_id:2,
								trade_info:'签到'
							}
						}]
					};
					const callback = (res) => {
						if (res.solely_code==100000) {
							self.showView = true;
							self.getUserData()
						}else{
							self.$Utils.showToast(res.msg,'none');
						}
					};
					self.$apis.logAdd(postData, callback);
				}
			},
			
			
			showAlert(){
				this.showView = true;
			},
			closeAlert(){
				this.showView = false;
			}
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	/* @import "../../assets/style/myCenter.css"; */
	page{background: #F5F5F5;position: relative;}
	/* header部分 */
	.container{height: 100%;overflow-y:scroll;padding-bottom: 80rpx;position: relative;}
	.signIn{width: 100%;left:0;top:40rpx;position: absolute;z-index: 1;}
	.signIn_box{padding: 0 30rpx;justify-content: flex-end;}
	.signIn_info_txt{color: #FFFFFF;font-size: 24rpx;}
	.mine{width: 690rpx;height: 200rpx;background: #FFFFFF;box-shadow: -1px -1px 8px #999999;border-radius: 30rpx;z-index: 1;box-sizing: border-box;justify-content: space-between;}
	.header_info{width: 100%;left:0;top:100rpx;position: absolute;z-index: 1;}
	.my_icon{width: 120rpx;height: 120rpx;border-radius: 50%;margin-left: 30rpx;margin-right: 20rpx;}
	.mine_info{height:100%;align-items: center;}
	.my_name{font-size: 28rpx;color: #212121;}
	.my_degree{width:90rpx;background: #FFD101;border-radius: 20rpx;text-align: center;color: #FFFFFF;font-size: 20rpx;height: 34rpx;line-height: 34rpx;}
	.mine_playgame{width:120rpx;height:50rpx;background: #FE546C;border-radius: 25rpx;text-align: center;color: #FFFFFF;font-size: 28rpx;line-height: 50rpx;margin-right: 30rpx;}
	/* list部分 */
	.my_list_title{padding: 30rpx;font-size: 28rpx;color: #212121;font-weight: bold;}
	.nav{width: 6rpx;height: 30rpx;background: #F15C73;}
	.list{width: 100%;padding-top: 100rpx;}
	.mytool{background: #FFFFFF;border-radius: 30rpx;margin: 0 30rpx;box-shadow: -1px -1px 8px #999999;}
	.my_list_box{padding: 40rpx 0;margin: 0 20rpx;justify-content: space-between;border-bottom: solid 1px #EAEAEA;}
	.title{margin-left: 20rpx;font-size: 26rpx;}
	.my_icon{justify-content: flex-end;}
	.mask{position: absolute;width: 100%;height: 100%;background: rgba(0,0,0,.8);left: 0;top: 0;z-index: 10;}
	.alertFcBox{flex-direction: column;position: absolute;left: 0;top: -30%;bottom: 0;right: 0;}
	.closeBtn{padding-top:100rpx;}
	.sucess_text{color: #ED6A81;position: absolute;left: 36%;top: 35%;bottom: 0;right: 0;z-index: 100;width: 100%;height: 50rpx;}
</style>
