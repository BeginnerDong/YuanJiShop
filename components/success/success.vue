<template>
	<view class="mask">
		
	</view>
</template>

<script>
	export default {
		data() {
			return{
				showView: false
			}
		},
		mounted:function(){
		},
		methods: {
			showAlert(){
				this.showView = true;
			},
			coloseAlert(){
				this.showView = false;
			},
		}
	}
</script>

<style scoped>
	@import "../../assets/style/public.css";
</style>