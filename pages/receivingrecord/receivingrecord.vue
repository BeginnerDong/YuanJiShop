<template>
	<view>
		<view style="width: 100%;height: 40rpx;"></view>
		<view class="container">
			<view style="width: 100%;height: 80rpx;"></view>
			<view class="container_item flex">
				<view class="container_item_left">姓名：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您的姓名" v-model="submitData.name" />
				</view>
			</view>
			<view style="width: 100%;height: 80rpx;"></view>
			<view class="container_item flex">
				<view class="container_item_left">电话：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您的手机号" v-model="submitData.phone" />
				</view>
			</view>
			<view style="width: 100%;height: 80rpx;"></view>
			<view class="container_item flex">
				<view class="container_item_left">地址：</view>
				<view class="container_item_right">
					<input type="text" placeholder="请输入您的地址" v-model="submitData.address" />
				</view>
			</view>
			<view style="width: 100%;height: 300rpx;"></view>
			<view class="confirm flex flexCenter" @click="submit">
				<view class="confirm_box">确定</view>
			</view>
			<view style="width: 100%;height: 80rpx;"></view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				webself: this,
				submitData: {
					name: '',
					phone: '',
					address: ''
				},
				userData: {}
			}
		},
		onLoad() {
			const self = this;

			var options = self.$Utils.getHashParameters();
			self.$Utils.loadAll(['getUserData'], self);
		},



		methods: {

			getUserData() {
				const self = this;
				const postData = {
					tokenFuncName: 'getProjectToken'
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0],
							self.submitData.name = self.userData.info.name,
							self.submitData.phone = self.userData.info.phone,
							self.submitData.address = self.userData.info.address
					}
					console.log('res', res)
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},

			submit() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = self.$Utils.cloneForm(self.submitData)

				if (self.$Utils.checkComplete(self.submitData)) {
					const callback = (res) => {
						if (res.solely_code == 100000) {
							self.$Utils.showToast('保存成功', 'none');
							setTimeout(function() {
								uni.navigateBack({
									delta:1
								})
							}, 1000);
						} else {
							self.$Utils.showToast(res.msg, 'none')
						}
					};

					self.$apis.userInfoUpdate(postData, callback);
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

	.container {
		margin: 0 30rpx;
		background: #FFFFFF;
	}

	.container_item {
		justify-content: space-between;
	}

	.container_item_left {
		text-align: center;
		flex: 1;
	}

	.container_item_right {
		background: #F5F5F5;
		width: 555rpx;
		height: 70rpx;
		margin-right: 30rpx;
	}

	.container_item_right>input {
		text-indent: 5%;
		width: 100%;
		height: 100%;
		line-height: 70rpx;
	}

	.confirm_box {
		width: 600rpx;
		height: 80rpx;
		background: #FF566D;
		letter-spacing: 10rpx;
		color: #FFFFFF;
		text-align: center;
		line-height: 80rpx;
		font-size: 30rpx;
		border-radius: 40rpx;
	}
</style>
