<template>
	<view style="width:100%">
		<c-tabbar></c-tabbar>
	</view>
</template>

<script>
	import cTabbar from "@/components/tabbar/tabbar.vue"
	
	export default {
		components: {
			cTabbar
		},
		data() {
			return {
				webself:this
			}
		},
		onLoad() {
			const self = this;
			console.log(88888)
			//self.$Utils.loadAll(['tokenGet'], self);
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
						uni.setStorageSync('token_expire_time',1565419588000)
					}
					console.log('res', res)
					self.$Utils.finishFunc('tokenGet');
				};
				self.$apis.tokenGet(postData, callback);
			},
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{background: #FFFFFF;}
</style>
