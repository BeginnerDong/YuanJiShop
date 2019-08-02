<template>
	<view class="container">
		
		<view class="content">
			<view :key="index" class="content_box flex flexCenter" v-for="(item,index) in my_list">
				<view style="width: 100%;height: 24rpx;"></view>
				<view class="content_item">
					<view style="width: 100%;height: 19rpx;"></view>
					<view class="content_item_time">{{item.record_time}}</view>
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="content_item_main flex">
						<view>
							<image class="item_icon" :src="item.record_src"></image>
						</view>
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="content_item_main_right">
							<view>
								<view style="width: 100%;height: 20rpx;"></view>
								<span class="item_name">{{item.record_name}}</span>
							</view>
							<view class="item_info">{{item.record_info}}</view>
						</view>
					</view>
					<view style="width: 100%;height: 50rpx;"></view>
				</view>
				<view style="width: 100%;height: 30rpx;"></view>
				<view class="recipientinfo">
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="recipientinfo_tit flex">
						<view class="recipientinfo_label " :class="type==1?'recipientinfo_label_actived':''" @click="changeType('1')">线上快递</view>
						<view style="width: 50rpx;height: 100%;"></view>
						<view class="recipientinfo_label" :class="type==2?'recipientinfo_label_actived':''" @click="changeType('2')">门店自营</view>
					</view>
					<view style="width: 100%;height: 50rpx;"></view>
					<view class="recipientinfo_info flex" v-if="type==1">
						<view class="flex">
							<image class="recipientinfo_info_icon" src="../../static/images/positioning-icon.png"></image>
							<view style="width: 30rpx;height: 100%;"></view>
							<view class="recipientinfo_info_msg">
								<view class="flex">
									<view class="recipientinfo_info_name item_name">张三</view>
								
									<view class="recipientinfo_info_tel">15632564563</view>
								</view>
								<view style="width: 100%;height: 30rpx;"></view>
								<view class="recipientinfo_info_address">陕西省西安市高新区大都荟</view>
							</view>
						</view>
						<view @click="webself.$Router.navigateTo({route:{path:'/pages/receivingrecord/receivingrecord'}})">
							<image style="width: 12rpx;height: 22rpx;" src="../../static/images/about-icon8.png"></image>
						</view>
					</view>
					
					<view class="recipientinfo_info flex" v-if="type==2">
						<view class="flex">
							<image class="recipientinfo_info_icon" src="../../static/images/positioning-icon.png"></image>
							<view style="width: 30rpx;height: 100%;"></view>
							<view class="recipientinfo_info_msg">
								<view class="flex">
									<view class="recipientinfo_info_name item_name">门店名称门店名称</view>
								</view>
								<view style="width: 100%;height: 30rpx;"></view>
								<view class="recipientinfo_info_address">地址：陕西省西安市高新区大都荟</view>
							</view>
						</view>
						<view  @click="webself.$Router.navigateTo({route:{path:'/pages/tothestore/tothestore'}})">
							<image style="width: 12rpx;height: 22rpx;" src="../../static/images/about-icon8.png"></image>
						</view>
					</view>
				</view>
				<view style="width: 100%;height: 250rpx;"></view>
				<view class="confirm">确认</view>
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
				type:1,
				webself:this,
				my_list: [
					{
						record_time:"2019-05-20",
						record_src:"../../static/images/record-img.png",
						record_name:"穿衣熊60cm",
						record_info:"商品价值=金币500/积分480"
					}
				]
			}
		},
		methods: {
			changeType(type){
				const self = this;
				if(self.type!=type){
					self.type = type
				}
			},
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{background: #F5F5F5;}
	.content{padding: 0 30rpx;}
	.content_box{flex-direction: column;}
	.content_item{width: 630rpx;height:250rpx;background: #FFFFFF;border-radius: 30rpx;padding: 0 30rpx;}
	.content_item_time{font-size: 24rpx;line-height: 24rpx;color: #999999;}
	.content_item_main_right{height:140rpx;display:flex;flex-direction: column;justify-content: space-between;}
	.item_icon{width: 140rpx;height: 140rpx;}
	.item_name{font-size: 28rpx;color: #222222;line-height: 28rpx;}
	.item_info{font-size: 22rpx;color: #666666;line-height: 22rpx;}
	.recipientinfo{width: 630rpx;height:261rpx;background: #FFFFFF;border-radius: 30rpx;padding: 0 30rpx;}
	.recipientinfo_tit{}
	.recipientinfo_label{width: 140rpx;height: 50rpx;border-radius: 25rpx;border: solid 1px #666666;text-align: center;line-height: 50rpx;box-sizing: border-box;}
	.recipientinfo_label_actived{background: #09C15F;border: none;color: #FFFFFF;}
	.recipientinfo_info{justify-content: space-between;}
	.recipientinfo_info_icon{width: 60rpx;height: 60rpx;}
	.recipientinfo_info_tel{font-size: 26rpx;color: #222222;line-height: 26rpx;opacity: .8;}
	.recipientinfo_info_name{}
	.recipientinfo_info_address{opacity: .9;font-size: 26rpx;color: #222222;line-height: 26rpx;}
	.confirm{width: 500rpx;height: 80rpx;background: #FF566D;color: #FFFFFF;text-align: center;line-height: 80rpx;font-size: 30rpx;border-radius: 40rpx;}
</style>

