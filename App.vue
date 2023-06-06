<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss">
	/* 注意要写在第一行，同时给style标签加入lang="scss"属性 */
	@import "@/uni_modules/uview-ui/index.scss";

	view,
	text {
		// 元素的宽度和高度包括了内容、边框和内边距的尺寸。设置的宽度和高度值将直接决定元素的实际宽度和高度，不会被边框和内边距所增加。
		box-sizing: border-box;
	}
</style>