<template>
	<view class="flex flexCenter tabbar" style="" >
		<view class="tabbar_item"  @click="Router.navigateTo({route:{path:'/pages/playgame/playgame'}})">
		    <view class="nav_title">进入游戏</view>
		</view>
		<view class="tabbar_item"  @click="Router.navigateTo({route:{path:'/pages/productsexchange/productsexchange'}})">
		    <view class="nav_title">兌换商城</view>
		</view>
		<view class="tabbar_item"  @click="Router.navigateTo({route:{path:'/pages/personage/personage'}})">
		    <view class="nav_title">个人中心</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			list: Array
		},
		
		data() {
			return {
				Router:this.$Router
			};
		},
		
		mounted:function(){
		},
		
		methods: {
		}
	}
</script>

<style scoped>
	@import "../../assets/style/public.css";
	.tabbar{
		width: 100%;
		height: 90rpx;
		line-height: 90rpx;
		position: fixed;
		bottom: 0;
		left: 0;
		background-color: white;
		border-top: solid 1px #EFEFEF;
	}
	.tabbar_item{
		flex: 1;
	}
	.nav_title{
		width:100%;
		font-size: 30rpx;
		text-align: center;
	}
</style>