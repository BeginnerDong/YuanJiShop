
<script>
	import token from "./common/token.js"
	export default {
		onLaunch: function() {	
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	@import "/assets/style/style.css";
	body, html {
		-webkit-user-select: none;
		user-select: none;
		width: 100%;
		min-height: 100%;
	}
	.ql-editor img{
		max-width: 100%;
		min-width: 50%;
		display: block;
		padding: 10px 0;
	}
</style>
