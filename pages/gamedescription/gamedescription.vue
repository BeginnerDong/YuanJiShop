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
							title: ['=', ['游戏说明']],
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
	.header{position: relative;}
	.header_img{width: 100%;height: 900rpx;}
	.header_txt{}
	.header_info{position: absolute;width: 100%;left: 1%;top: 27%;}
	.header_info_box{width: 600rpx;height:480rpx;color: #70585c;overflow: hidden;font-size: 26rpx;}
	.show{padding: 0 30rpx;}
	.show_img_1{width: 100%;height: 825rpx;}
	.show_img_2{width: 100%;height: 1425rpx;}
</style>
