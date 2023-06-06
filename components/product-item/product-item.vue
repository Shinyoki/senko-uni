<template>
	<view class="product-item">
		<!-- 产品图 -->
		<view class="pic">
			<image class="img" src="../../static/logo.png" mode="aspectFill"></image>
		</view>
		<!-- 右侧 -->
		<view class="product-content">
			<view class="title">产品标题</view>
			<view class="price">
				<view class="big">￥10.5</view>
				<view class="small">￥22.5</view>
			</view>
			<view class="discount">3折</view>
			<view class="number">
				<view class="sku-select" v-if="false">选规格</view>
				<view class="u-num" v-else>
					<pro-num-box></pro-num-box>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "product-item",
		data() {
			return {
			};
		},
	}
</script>

<style lang="scss">
	.product-item {
		width: 100%;
		height: 200rpx;

		@include flex-box-set(between, center) margin: 50rpx 0;

		.pic {
			width: 180rpx;
			height: 180rpx;
			border-radius: 20rpx;
			overflow: hidden;

			margin-left: 10rpx;

			.img {
				width: 100%;
				height: 100%;
			}
		}

		.product-content {
			flex: 1;
			padding-left: 20rpx;
			position: relative;

			.title {
				font-size: 34rpx;
				font-weight: bold;

				@include ellipsis;
			}

			.price {
				display: flex;
				font-weight: bold;
				padding: 25rpx 0;

				.big {
					font-size: 34rpx;
					color: $brand-theme-color;
				}

				.small {
					font-size: 26rpx;
					opacity: 0.4;
					text-decoration: line-through;
					padding-left: 10rpx;
				}
			}

			.discount {
				font-size: 22rpx;
				color: $brand-theme-color;
				padding: 3rpx 8rpx;
				border: 1rpx solid $brand-theme-color;
				display: inline;
				border-radius: 6rpx;
			}

			.number {
				position: absolute;
				right: 0;
				bottom: 0;

				.sku-select {
					height: 40rpx;
					padding: 0 10rpx;
					background: $brand-theme-color;
					font-size: 28rpx;
					color: #fff;
				}

			}
		}
	}
</style>