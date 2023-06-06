<template>
	<view class="home">
		<!-- 头部图像 -->
		<customer-headbar></customer-headbar>
		<!-- 中心主体 -->
		<view class="wrapper">
			<view class="info-model">
				<view class="left">免费配送</view>
				<view class="right">
					<u-icon name="order" color="#576b95" size="16"></u-icon>
					我的订单
				</view>
			</view>
			<!-- 滑动内窗 -->
			<view class="scroll-layout">
				<view class="left-scroll">
					<scroll-view scroll-y class="s-content">
						<!-- 选项 -->
						<view :class="['nav-item', index == currentIndex ? 'active' : '']" v-for="(item, index) in 50"
							@click="clickNav(index)">
							{{ item }}
						</view>
					</scroll-view>
				</view>
				<view class="right-scroll">
					<!-- 搜索 -->
					<view class="right-scroll-search">
						<u-icon name="search"></u-icon>搜索
					</view>

					<scroll-view scroll-y class="s-content" @scroll="rightScrollEvent" :scroll-top="scrollTop"
						scroll-with-animation>
						<view class="pro-view" v-for="item in 5">
							<!-- 选项对应的标签 -->
							<u-sticky :custom-nav-height="0" z-index="2">
								<view class="pro-title">产品名称{{item}}</view>
							</u-sticky>
							<view class="pro-content">
								<view class="pro-item">
									<product-item v-for="i in 5"></product-item>
								</view>
							</view>
						</view>
					</scroll-view>
				</view>
			</view>
		</view>
		<!-- 底部 -->
		<view style="height: 100rpx; background-color: green;"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				count: 0,
				currentIndex: 0,
				scrollTop: 0,
				leftScrollValue: 0,
				rightScrollValue: 0,
				rightHitArr: [],
				leftHitArr: [],
				lastClickNavTimestamp: 0
			}
		},
		onLoad() {
			this.$nextTick(() => {
				this.getHeightArr();
			})
		},
		methods: {
			clickNav(index) {
				if (this.currentIndex == index) return;
				// 如果500毫秒前点击过，就不修改cIndex,防止点击速度过快，动画跟不上
				if (Date.now() - this.lastClickNavTimestamp < 500) return;
				this.currentIndex = index;
				this.lastClickNavTimestamp = Date.now();
				this.scrollTop = this.rightHitArr[index];

			},
			rightScrollEvent(e) {
				this.scrollTop = e.detail.scrollTop
				let index = this.rightHitArr.findIndex(item => item > this.scrollTop);
				if (index == -1) index = this.rightHitArr.length - 1;
				this.currentIndex = index - 1 > 0 ? index - 1 : 0;

			},
			getHeightArr() {
				let selectorQuery = uni.createSelectorQuery();
				let customHeadBar;
				//获取自定义导航高度				
				selectorQuery.select(".info-model").boundingClientRect(rect => {
					customHeadBar = rect.height;
				}).exec()

				//左侧滚到区域的节点组
				selectorQuery.selectAll(".nav-item").boundingClientRect(rects => {
					this.leftHitArr = rects.map(item => item.top - customHeadBar - 40)
				}).exec()
				console.log(this.leftHitArr);
				//右侧滚到区域的节点组
				selectorQuery.selectAll(".pro-view").boundingClientRect(rects => {
					this.rightHitArr = rects.map(item => item.top - customHeadBar - 40)
				}).exec()

			},
		},
		computed: {

		},
		watch: {

		}
	}
</script>

<style lang="scss">
	.home {
		height: 100vh;
		display: flex;
		flex-direction: column;

		.wrapper {
			flex: 1;
			background: $border-color-light;

			border-radius: 20rpx 20rpx 0 0;
			margin-top: -20rpx;
			position: relative;
			z-index: 2;
			overflow: hidden;

			.info-model {
				color: $text-font-color-1;

				@include flex-box;

				height: 90rpx;
				background: #fff;
				padding: 0 30rpx;
				border-bottom: 1px solid $border-color;

				font-size: 32rpx;

				.right {
					@include flex-box();

					color: $text-font-color-2;
				}
			}

			.scroll-layout {
				height: calc(100% - 100rpx);
				@include flex-box;

				.left-scroll {
					height: 100%;
					width: 196rpx;

					border-right: 1px solid $border-color;
					background: $page-bg-color;

					.nav-item {
						font-size: 30rpx;
						padding-left: 30rpx;
						line-height: 100rpx;
						color: $text-font-color-2;
						position: relative;

						&.active {
							color: $text-font-color-1;
							background-color: #fff;

							&::after {
								content: "";
								width: 6rpx;
								height: 30rpx;
								background-color: $brand-theme-color;

								position: absolute;
								left: 5rpx;
								top: 50%;
								transform: translateY(-50%);
							}
						}
					}
				}

				.right-scroll {
					height: 100%;
					flex: 1;

					position: relative;

					.pro-view {
						padding: 0 30rpx;

						.pro-title {
							line-height: 90rpx;
						}
					}

					.right-scroll-search {
						position: absolute;

						@include flex-box-set;
						z-index: 3;
						right: 0;

						height: 90rpx;
						color: $brand-theme-color-aux;
					}
				}

				.s-content {
					height: 100%;
				}


			}
		}
	}
</style>