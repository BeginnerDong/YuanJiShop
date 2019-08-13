<template>
	<view class="container">
		<view class="content ql-editor" v-html="mainData.content">
		</view>
	</view>
</template>

<script>
	export default {
		
		data() {
			return {
				mainData:{},
				webself:this,
			
			}
		},
		
		onLoad() {		
			const self = this;
			
			var options = self.$Utils.getHashParameters();	
			self.$Utils.loadAll(['getMainData'], self);			
		},
		
		
		methods: {
			
			
			getMainData() {
				const self = this;
				const postData = {
					searchItem:{
						thirdapp_id:2
					}			
				};
				postData.getBefore = {
					article: {
						tableName: 'Label',
						searchItem: {
							title: ['=', ['加盟说明']],
						},
						middleKey: 'menu_id',
						key: 'id',
						condition: 'in',
					},
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0]	
					}
					console.log('res', res)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{background: #F5F5F5;}
	.container{height: 100%;flex-direction: column;}
	.logo{width:100%; text-align: center;}
	.content{padding: 0 30rpx;}
	.content_title{font-size: 26rpx;color: #212121;font-weight: bold;line-height: 26rpx;}
	.paragraph{font-size: 24rpx;color: #212121;}
</style>
