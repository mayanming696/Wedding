<template>
	<div class="componentsWarp">
		<div class="wedding-invitation" :class="{ 'invitation-bounce':canOpen }">
			<div class="invitation-container" :class="{ 'invitation-down':isOpening }">
				<div class="invitation-cover">
					<div class="cover-content" :class="{'invitation-up':isOpening}">
						<div class="content-inside" v-if="isOpening">
							<swiper class="swiper" :indicator-dots="false" :autoplay="true" indicator-dots
								indicator-color="#a2b6a4" indicator-active-color="#1c5648"
								easing-function="easeOutCubic">
								<swiper-item>
									<image mode="aspectFit" class="content-inside-photo"
										src="https://cdn.jsdelivr.net/gh/mayanming696/CDN/wedding/photo1.jpg">
								</swiper-item>
								<swiper-item>
									<image mode="aspectFit" class="content-inside-photo"
										src="https://cdn.jsdelivr.net/gh/mayanming696/CDN/wedding/photo6.jpg">
								</swiper-item>
								<swiper-item>
									<image mode="aspectFit" class="content-inside-photo"
										src="https://cdn.jsdelivr.net/gh/mayanming696/CDN/wedding/photo2.jpg">
								</swiper-item>
								<swiper-item>
									<image mode="aspectFit" class="content-inside-photo"
										src="https://cdn.jsdelivr.net/gh/mayanming696/CDN/wedding/photo3.jpg">
								</swiper-item>
								<swiper-item>
									<image mode="aspectFit" class="content-inside-photo"
										src="https://cdn.jsdelivr.net/gh/mayanming696/CDN/wedding/photo4.jpg">
								</swiper-item>
								<swiper-item>
									<image mode="aspectFit" class="content-inside-photo"
										src="https://cdn.jsdelivr.net/gh/mayanming696/CDN/wedding/photo5.jpg">
								</swiper-item>
							</swiper>
							<p><span style="font-weight:bold;">Marco & June</span></p>
							<div class="saveDate" :style="{backgroundImage: `url(${imageURL})`}">
								<!-- <image class="saveImage" mode="aspectFit" src="../images/titlewrap.png"></image> -->
								<p style="font-weight:bold;">2021-12-25</p>
							</div>
							<p>地点：<span style="font-weight:bold;">深圳市坪山区我愿意咖啡屋</span></p>
							<div class="content-inside-bless">
								<div style="margin-top: 50upx;">
									<button @tap="closeInvitation">关 闭</button>
								</div>
							</div>
						</div>
					</div>
					<div class="cover-inside-left" :class="{'opening':isOpening}">
						<image class="logoImage" mode="aspectFit"
							src="https://cdn.jsdelivr.net/gh/mayanming696/CDN/wedding/logo.png"></image>
					</div>
					<div class="cover-inside-right" :class="{'opening':isOpening}"></div>
					<img class="cover-inside-seal" src="@/images/seal.png" @tap="openInvitation"
						:class="{'invitation-flight':isOpening}">
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		props: ['canOpen'],
		data() {
			return {
				isOpening: false,
				wish: '',
				isFocused: false,
				hasEntered: false,
				imageURL: 'https://cdn.jsdelivr.net/gh/mayanming696/CDN/wedding/titlewrap.png'
			}
		},
		methods: {
			// 打开邀请函
			openInvitation() {
				this.isOpening = true
			},
			closeInvitation() {
				this.isOpening = false
				setTimeout(() => {
					this.$emit('onClose')
				}, 800)
			},
		}
	}
</script>

<style lang="less" scoped>
	@keyframes logoHeader {
		0% {
			transform: rotate(-15deg) scale(0.8, 0.8);
			opacity: 1;
		}

		25% {
			transform: rotate(-15deg) scale(1, 1);
			opacity: 0.8;
		}

		100% {
			transform: rotate(-15deg) scale(0.8, 0.8);
			opacity: 1;
		}
	}

	.componentsWarp {
		height: 100%;
		width: 100%;
		position: fixed;
		left: 0;
		top: 0;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.wedding-invitation {
		position: absolute;
		top: 100upx;
		left: 30upx;
		width: calc(100% - 60upx);
		height: calc(100% - 250upx);
		z-index: 4;
		transform: scale(0.05);
		opacity: 0;
		transition: transform 0.8s cubic-bezier(.26, 1.84, .39, .61), opacity 0.5s linear;
		background-size: 100%;
		margin: auto;

		&.invitation-bounce {
			opacity: 1;
			transform: scale(1);
		}

		.invitation-container {
			position: relative;
			width: 100%;
			height: 100%;
			transition: transform 0.6s cubic-bezier(0.4, 0, 1, 1);

			&.invitation-down {
				transform: translateY(40upx);
			}

			.invitation-cover {
				width: 94%;
				height: 100%;
				background-color: #D65047;
				border-radius: 20upx;
				perspective: 500px;
				box-shadow: 0 0 20upx 2upx rgba(0, 0, 0, 0.15);
				margin: auto;

				.cover-content {
					height: 100%;
					padding: 20upx 40upx;
					transition: transform 0.8s cubic-bezier(0.4, 0, 1, 1);
					overflow: hidden;

					&.invitation-up {
						transform: translateY(-80upx);
					}

					.content-inside {
						display: flex;
						flex-direction: column;
						align-items: center;
						border-radius: 20upx;
						height: calc(100% - 80upx);
						padding: 35upx;
						color: #544c37;
						background-color: #f1ede2;
						text-align: center;
						overflow: hidden;
						z-index: 9999;

						.saveDate {
							width: 100;
							display: flex;
							flex-direction: column;
							justify-content: center;
							align-items: center;
							background-size: cover;
							background-position: center center;
							background-size: 100% 100%;
							width: 100%;
							height: 130upx;

							>p {
								margin-top: 40upx;
							}
						}

						.swiper {
							width: 100%;
							height: 40%;
							display: flex;
							flex-direction: row;
							align-items: center;
							justify-content: center;
							margin-bottom: 20upx;
							padding: 5px;
							border: 4upx solid #f7debb;
							z-index: 3;
						}

						.content-inside-photo {
							width: 100%;
							height: 100%;
							z-index: 2 !important;
						}

						p {
							display: flex;
							margin-top: 0;
							word-break: keep-all;
							white-space: nowrap;
							font-size: 30upx;
						}

						.content-inside-bless {
							>div {
								display: flex;

								button {
									width: 100%;
									height: 60upx;
									font-size: 30upx;
									line-height: 60upx;
									color: #a9895d;
									background: #f7debb;
									border: none;
									outline: none;

									&:disabled {
										opacity: 0.8;
									}

									&:first-child {
										margin-right: 10px;
										flex: 1;
									}

									&:last-child {
										width: 200upx;
										opacity: 0.8;
										border: 1px solid #f7debb;
										color: #f1ede2;
										background: #D65047;
									}
								}
							}
						}
					}
				}

				.cover-inside-left {
					position: absolute;
					left: 0;
					top: 0;
					width: 70%;
					height: 100%;
					border-radius: 10px;
					background-color: #f3f0e6;
					box-shadow: 5px 0 10px rgba(0, 0, 0, 0.2);
					z-index: 6;
					transition: transform 0.5s;
					transform-origin: 0 50%;

					.logoImage {
						width: 250upx;
						height: 250upx;
						transform: rotate(-15deg);
						animation: logoHeader 1s infinite;
					}

					&.opening {
						transform: rotate3d(0, 1, 0, -140deg);
					}
				}

				.cover-inside-right {
					position: absolute;
					right: 0;
					top: 0;
					width: 40%;
					height: 100%;
					border-radius: 10px;
					// background-color: #D65047;
					background-color: #f3f0e6;
					box-shadow: -5px 0 10px rgba(0, 0, 0, 0.2);
					z-index: 5;
					transition: transform 0.5s;
					transform-origin: 100% 50%;

					&.opening {
						transform: rotate3d(0, 1, 0, 140deg);
					}
				}

				.cover-inside-seal {
					position: absolute;
					left: 70%;
					bottom: 100px;
					width: 80px;
					height: 80px;
					margin-left: -40px;
					z-index: 7;
					transform-origin: 50% 50%;
					transition: all 0.8s cubic-bezier(0.4, 0, 1, 1);

					&.invitation-flight {
						opacity: 0;
					}
				}
			}
		}
	}
</style>
