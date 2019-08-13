<template>
	<view>
		<view style="width: 100%;height: 30rpx;"></view>
		<view class="applyforjoining_title flex">
			<view class="lotteryexplain flex" @click="webself.$Router.navigateTo({route:{path:'/pages/joinexplain/joinexplain'}})">
				<image style="width:30rpx;height: 30rpx;margin-right: 10rpx;" src="../../static/images/join-icon0.png"></image>
				<span>加盟说明</span>
			</view>
		</view>
		<view style="width: 100%;height: 30rpx;"></view>
		<view class="container">
			<view class="container_item flex">
				<view class="container_item_left">选择类型：</view>
				<view class="container_item_right flex">
					<view class="recipientinfo_tit flex">
						<view class="recipientinfo_label" 
						:class="submitData.class==1?'recipientinfo_label_actived':''" @click="changeClass('1')">单店加盟</view>
						<view style="width: 50rpx;height: 100%;"></view>
						<view class="recipientinfo_label" 
						:class="submitData.class==2?'recipientinfo_label_actived':''"  @click="changeClass('2')">城市加盟</view>
					</view>
				</view>
			</view>
			<view class="container_item flex">
				<view class="container_item_left">姓名：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您的姓名" v-model="submitData.title"/>
				</view>
			</view>
			<view class="container_item flex">
				<view class="container_item_left">手机号：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您的手机号" v-model="submitData.phone"/>
				</view>
			</view>
			<view class="container_item flex">
				<view class="container_item_left">所在城市：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您所在的城市" v-model="submitData.description"/>
				</view>
			</view>
		</view>
		<view style="width: 100%;height: 200rpx;"></view>
		<view class="confirm flex flexCenter" @click="submit">
			<view class="confirm_box">提交信息</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				webself: this,
				submitData: {
					class: 1,
					title: '',
					phone: '',
					description: '',
					type:1
				}
			}
		},
		onLoad() {
			const self = this;
			var options = self.$Utils.getHashParameters();
			
		},



		methods: {

			changeClass(num){
				const self = this;
				if(self.submitData.class!=num){
					self.submitData.class = num
				}
			},

			submit() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = self.$Utils.cloneForm(self.submitData)

				if (self.$Utils.checkComplete(self.submitData)) {
					const callback = (res) => {
						if (res.solely_code == 100000) {
							self.$Utils.showToast('提交成功', 'none');
							self.submitData={
								class: 1,
								title: '',
								phone: '',
								description: ''
							}
						} else {
							self.$Utils.showToast(res.msg, 'none')
						}
					};

					self.$apis.messageAdd(postData, callback);
				} else {
					self.$Utils.showToast('请补全信息', 'none')
				};
			},

		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");

	page {
		background: #F5F5F5;
	}

	.applyforjoining_title {
		height: 30rpx;
		justify-content: flex-end;
		color: #EE9CA7;
		padding: 0 30rpx;
	}

	.recipientinfo_label {
		width: 140rpx;
		height: 50rpx;
		border-radius: 25rpx;
		border: solid 1px #EE9CA7;
		text-align: center;
		line-height: 50rpx;
		box-sizing: border-box;
	}

	.recipientinfo_label_actived {
		background: #F8546B;
		border: none;
		color: #FFFFFF;
	}

	.container {
		margin: 0 30rpx;
		background: #FFFFFF;
		padding: 0 30rpx;
	}

	.container_item {
		border-bottom: solid 1px #EAEAEA;
		padding: 30rpx 0;
	}

	.container_item_right {
		width: 60%;
		height: 70rpx;
		padding: 0 30rpx;
	}

	.container_item_right>input {
		text-indent: 5%;
		width: 100%;
		height: 100%;
		font-size: 24rpx;
		line-height: 70rpx;
	}

	.confirm_box {
		width: 600rpx;
		height: 80rpx;
		background: #FF566D;
		color: #FFFFFF;
		text-align: center;
		line-height: 80rpx;
		font-size: 30rpx;
		border-radius: 40rpx;
	}
</style>
