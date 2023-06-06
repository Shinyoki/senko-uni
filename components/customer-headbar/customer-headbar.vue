<template>
	<view class="custom-head">
		<view class="bg">
			<image class="bg-img" src="../../static/fengjing.png" mode="aspectFill"></image>
		</view>
	</view>
</template>

<script>
	export default {
		name:"customer-headbar",
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss">
.custom-head {
	height: 200rpx;
	overflow: hidden;
	.bg {
		width: 100%;
		height: 100%;
		background: #000;
		.bg-img {
			width: 100%;
			height: 100%;
			
			filter: blur(12rpx);
			transform: scale(1.5);
		}
	}
}
</style>