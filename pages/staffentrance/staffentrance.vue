<template>
	<view>
		<view class="container">
			<!-- header部分 -->
			<view class="header">
				<view class="header_info clearfix flex flexCenter">
					<view class="mine flex">
						<view class="mine_info flex flexCenter">
							<view class="mine_info_logo">
								<image class="my_icon" src="../../static/images/about-img.png"></image>
							</view>
							<view style="width: 100%;height: 10rpx;"></view>
							<view class="my_word">快乐猫</view>
							<view style="width: 100%;height: 20rpx;"></view>
							<view class="my_word mine_money">我的余额 ： 300</view>
						</view>
					</view>
				</view>
				<view class="signIn">
					<view class="signIn_box flex">
						<view class="signIn_info flex" @click="webself.$Router.navigateTo({route:{path:'/pages/basicinfo/basicinfo'}})">
							<image style="width: 26rpx;height: 26rpx;margin-right: 10rpx;" src="../../static/images/agent-icon5.png" mode=""></image>
							<span class="signIn_info_txt">基础信息</span>
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
			</view>
		</view>
		<!--浮窗-->
		<view class="mask" v-if="showView">
			<span class="sucess_text">恭喜获得10金币~</span>
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
				showView: false,
				webself:this,
				my_list:[
					{
						"my_src":"../../static/images/agent-icon2.png",
						"my_title":"我的商家",
						"my_key":"mybusiness"
					},
					{
						"my_src":"../../static/images/about-icon3.png",
						"my_title":"流水记录",
						"my_key":"flowrecord"
					},
					{
						"my_src":"../../static/images/about-icon4.png",
						"my_title":"佣金记录",
						"my_key":"commissionrecord"
					}
				]
			}
		},
		methods: {
			goPage(id) {
			    if(id=="mybusiness"){
					this.$Router.navigateTo({route:{path:'/pages/mybusiness/mybusiness'}});
				}else if(id=="flowrecord"){
					this.$Router.navigateTo({route:{path:'/pages/flowrecord/flowrecord'}});
				}else if(id=="commissionrecord"){
					this.$Router.navigateTo({route:{path:'/pages/commissionrecord/commissionrecord'}});
				}
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
	.mine{width: 690rpx;height: 272rpx;background: #FFFFFF;box-shadow: -1px -1px 8px #999999;z-index: 1;box-sizing: border-box;justify-content: space-between;border-radius: 30rpx;}
	.mine_info{width: 100%;flex-direction: column;}
	.header_info{width: 100%;left:0;top:100rpx;position: absolute;z-index: 1;}
	.my_icon{width: 120rpx;height: 120rpx;border-radius: 50%;margin-left: 30rpx;margin-right: 20rpx;}
	.mine_money{color: #E29A9A;}
	.my_word{font-size: 26rpx;line-height: 26rpx;}
	/* list部分 */
	.my_list_title{padding: 30rpx;font-size: 28rpx;color: #212121;font-weight: bold;}
	.nav{width: 6rpx;height: 30rpx;background: #F15C73;}
	.list{width: 100%;padding-top: 180rpx;}
	.mytool{background: #FFFFFF;border-radius: 30rpx;margin: 0 30rpx;box-shadow: -1px -1px 8px #999999;}
	.my_list_box{padding: 40rpx 0;margin: 0 20rpx;justify-content: space-between;border-bottom: solid 1px #EAEAEA;}
	.title{margin-left: 20rpx;font-size: 26rpx;}
	.my_icon{justify-content: flex-end;}
</style>
