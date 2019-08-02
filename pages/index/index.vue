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
			//self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			
		},
	};
</script>

<style scoped>
	@import url("../../assets/style/public.css");
	page{background: #FFFFFF;}
</style>
