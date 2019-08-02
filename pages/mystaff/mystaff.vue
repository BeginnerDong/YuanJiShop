<template>
	<view class="container">
		<!-- header部分 -->
		<view class="header flex flexCenter">
			<view class="header_centerbox flex">
				<view class="num">15</view>
				<view style="width: 100%;height: 50rpx;"></view>
				<view class="unit">个</view>
			</view>
		</view>
		<view style="width: 100%;height: 30rpx;"></view>
		<!-- list部分 -->
		<view class="list">
			<view class="list_item" v-for="(item,index) in my_list" :key="index">
				<view class="list_item_info">
					<view style="width: 100%;height: 20rpx;"></view>
					<view class="del flex">
						<view class="del_box flex"  @click="showdelAlert" >
							<image class="del_icon" src="../../static/images/delete-icon.png"></image>
							<span>删除</span>
						</view>
					</view>
					<view class="list_item_left_info flex">
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="item_tit">账号 : </view>
						<view style="width: 60rpx;height: 100%;"></view>
						<view class="item_main">{{item.my_list_acount}}</view>
					</view>
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="list_item_left_info flex">
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="item_tit">名称 : </view>
						<view style="width: 60rpx;height: 100%;"></view>
						<view class="item_main">{{item.my_list_name}}</view>
					</view>
					<view style="width: 100%;height: 30rpx;"></view>
					<view class="list_item_left_info flex">
						<view style="width: 30rpx;height: 100%;"></view>
						<view class="item_tit">电话 : </view>
						<view style="width: 60rpx;height: 100%;"></view>
						<view class="item_main">{{item.my_list_tel}}</view>
					</view>
					<view style="width: 100%;height: 40rpx;"></view>
				</view>
				<view style="width: 100%;height: 30rpx;"></view>
			</view>
			<view style="width: 100%;height: 30rpx;"></view>
		</view>
		<view class="addstaff" @click="showAlert">
			<view class="addstaff_box flex flexCenter">
				<span>添加员工</span>
			</view>
		</view>
		<!--加入员工浮窗-->
		<view class="mask" v-if="showView">
			<view class="alertFcBox flex flexCenter" v-if="showView">
				<view class="mystaff_info">
					<view style="width: 100%;height: 20rpx;"></view>
					<view class="close flex">
						<img class="closeBtn" @click="closeAlert" src="../../static/images/wrong-icon.png" alt="">
					</view>
					<view style="width: 100%;height: 40rpx;"></view>
					<view class="mystaff_info_item flex">
						<view class="item_left">账号：</view>
						<view class="item_right">
							<input type="text" placeholder="请输入您要添加的账号" />
						</view>
					</view>
					<view style="width: 100%;height: 80rpx;"></view>
					<view class="mystaff_info_item flex">
						<view class="item_left">密码：</view>
						<view class="item_right">
							<input type="text" placeholder="请输入密码" />
						</view>
					</view>
					<view style="width: 100%;height: 150rpx;"></view>
					<view class="confirm flex flexCenter">
						<view class="confirm_box" @click="closeAlert" >确定</view>
					</view>
					<view style="width: 100%;height: 80rpx;"></view>
				</view>
			</view>
		</view>
		<!-- 删除员工浮窗 -->
		<view class="mask" v-if="showdelstaff">
			<view class="alertFcBox flex flexCenter" v-if="showdelstaff">
				<view class="delstaff_info">
					<view style="width: 100%;height: 20rpx;"></view>
					<view class="close flex">
						<img class="closeBtn" @click="closedelAlert" src="../../static/images/wrong-icon.png" alt="">
					</view>
					<view style="width: 100%;height: 40rpx;"></view>
					<view class="flex flexCenter">是否确认删除该员工?</view>
					<view style="width: 100%;height: 80rpx;"></view>
					<view class="flex">
						<view class="select flex flexCenter">
							<view class="box yes" @click="closedelAlert" >是</view>
						</view>
						<view class="select flex flexCenter">
							<view class="box no" @click="closedelAlert" >否</view>
						</view>						
					</view>
					<view style="width: 100%;height: 80rpx;"></view>
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
				showView: false,
				showdelstaff:false,
				my_list:[
					{
						"my_list_acount":"15698563220",
						"my_list_name":"哆啦A梦",
						"my_list_tel":"15698563220",
						"my_red":false
						
					},
					{
						"my_list_acount":"15698563220",
						"my_list_name":"哆啦A梦",
						"my_list_tel":"15698563220",
						"my_red":false
						
					},
					{
						"my_list_acount":"15698563220",
						"my_list_name":"哆啦A梦",
						"my_list_tel":"15698563220",
						"my_red":false
						
					}
				]
			}
		},
		methods: {
			showAlert(){
				this.showView = true;
			},
			closeAlert(){
				this.showView = false;
			},
			showdelAlert(){
				this.showdelstaff = true;
			},
			closedelAlert(){
				this.showdelstaff = false;
			}
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{background: #F5F5F5;position: relative;}
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
	.del{justify-content: flex-end;padding: 0 20rpx 0 30rpx;}
	.del_icon{width: 32rpx;height: 30rpx;margin-right: 10rpx;}
	.addstaff{position: fixed;bottom: 20%;right: 0;}
	.addstaff_box{color: #FFFFFF;background: #F14667;width: 100rpx;height: 100rpx;border-radius: 50%;}
	.addstaff_box>span{width:80%;flex-wrap: wrap;text-align: center;}
	/* 加入员工浮窗 */
	.mask{position: absolute;width: 100%;height: 100%;background: rgba(0,0,0,.8);left: 0;top: 0;z-index: 10;}
	.alertFcBox{flex-direction: column;position: absolute;left: 0;top: -10%;bottom: 0;right: 0;}
	.close{justify-content: flex-end;}
	.closeBtn{width: 34rpx;height: 34rpx;}
	.mystaff_info{width: 630rpx;background: #FFFFFF;padding: 0 30rpx;border-radius: 20rpx;}
	.item_left{width: 20%;text-align: center;}
	.item_right{background: #F5F5F5;width: 555rpx;height: 70rpx;margin-right: 30rpx;}
	.item_right>input{text-indent: 5%;width: 100%;height: 100%;font-size: 24rpx;}
	.confirm_box{width: 600rpx;height: 80rpx;background: #FF566D;letter-spacing: 10rpx;color: #FFFFFF;text-align: center;line-height: 80rpx;font-size: 30rpx;border-radius: 20rpx;}
	.delstaff_info{width: 630rpx;background: #FFFFFF;padding: 0 30rpx;border-radius: 20rpx;}
	.select{flex: 1;}
	.box{width: 120rpx;height: 50rpx;border-radius: 25rpx;text-align: center;line-height: 50rpx;color: #FFFFFF;}
	.yes{background: #E29A9A;}
	.no{background: #E3E3E3;}
</style>
