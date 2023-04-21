<template>
	<view>
		<div class="draw-box" v-show="active">
			<!--背景光-->
			<div class="bg-light pic-rotate" style="background: url(/static/light.png) center no-repeat;
			width: 452px;
			height: 510px;
			z-index: 1;
			position: absolute;
			left: calc((100% - 452px) / 2);"></div>
			<!--宝箱-->
			<div :class="[opening ? 'pic-shake' : '', isOpen ? 'box-open' : '', 'close-box']" @click="openBox" style="background: url(/static/chest.png) 0px 0px no-repeat;
			background-size: 320px auto;
			width: 320px;
			height: 138px;
			z-index: 2;
			position: absolute;
			left: calc((100% - 320px) / 2);
			top: 180px;">
				<!--提示信息-->
				<div class="box-msg" v-show="confirmFlag">
					<!--中奖-->
					<div class="winning">
						<h3 class="box-msg-title">开箱成功</h3>
						<div class="box-msg-congent">恭喜您获得一张新的卡片，请继续加油！</div>
						<div class="box-msg-operat">
							<button type="button" class="btn-blue" @click="openNow">立即查看({{count}})</button>
						</div>
					</div>
				</div>
			</div>
			<!--提示操作-->
			<div class="prompt-operation">点击打开宝箱</div>
		</div>
		<view class="imgBox" v-show="!active">
			<image class="logo" src="/static/img1.jpg"></image>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				active: true,
				confirmFlag: false,
				opening: false,
				isOpen: false,
				count: 3,
				timer: null,
			}
		},
		onLoad() {
			// this.active = true;
			// setTimeout(() => {
			// 	this.active = false;
			// }, 2000);
		},
		methods: {
			openBox() {
				this.opening = true;
				setTimeout(() => {
					this.isOpen = true;
					setTimeout(() => {
						this.confirmFlag = true;
						this.reStart();
					}, 500);
				}, 1200);
			},
			reStart() {
				this.timer = setInterval(() => {
					this.count -= 1;
					if (this.count === 0) {
						this.active = false;
						this.confirmFlag = false;
						this.opening = false;
						this.isOpen = false;
						clearInterval(this.timer)
					}
				}, 1000)
			},
			openNow() {
				this.active = false;
				this.confirmFlag = false;
				this.opening = false;
				this.isOpen = false;
				clearInterval(this.timer)
			}
		}
	}
</script>

<style>
	.imgBox {
		height: 100vh;
		width: 100vw;
	}

	.logo {
		width: 100%;
		height: 100%;
	}

	* {
		padding: 0px;
		margin: 0px;
	}

	body {
		overflow: hidden;
	}

	.draw-box {
		width: 100%;
	}

	.bg-light {
		/* background: url(/static/light.png) center no-repeat;
		width: 452px;
		height: 510px;
		z-index: 1;
		position: absolute;
		left: calc((100% - 452px) / 2); */
	}

	.bg-light.pic-rotate {
		-webkit-animation: pic-rotate 10s infinite linear;
	}

	.close-box {
		/* background: url(/static/chest.png) 0px 0px no-repeat;
		background-size: 320px auto;
		width: 320px;
		height: 138px;
		z-index: 2;
		position: absolute;
		left: calc((100% - 320px) / 2);
		top: 180px; */
	}

	.close-box.box-open {
		/* background: url(/static/chest.png) 0px -139px no-repeat;
		background-size: 320px auto;
		width: 320px;
		height: 138px;
		z-index: 2;
		position: absolute;
		left: calc((100% - 320px) / 2);
		top: 180px; */
	}

	.close-box.pic-shake {
		-webkit-animation: pic-shake 1.2s linear;
	}

	.box-msg {
		width: 80%;
		height: auto;
		margin: 0px auto;
		border: 5px solid #fce92f;
		background-color: rgba(255, 255, 255, 0.8);
		position: relative;
		top: -100px;
		box-shadow: 1px 1px 3px #888888;
		border-radius: 10px;
		padding: 10px;
		z-index: 5;
	}

	.hide {
		display: none;
	}

	.box-msg-title {
		text-align: center;
		margin: 0px 0px 10px 0px;
	}

	.box-msg-congent {
		line-height: 28px;
		margin: 0px 0px 10px 0px;
		color: #610c03;
	}

	.box-msg-tip {
		font-size: 12px;
		color: #333333;
	}

	.box-msg-operat {
		text-align: center;
	}

	.btn-blue {
		border: none;
		background-color: #fce92f;
		padding: 3px 15px;
		border-radius: 5px;
		box-shadow: 1px 1px 3px #888888;
	}

	.prompt-operation {
		width: 100%;
		position: absolute;
		top: 350px;
		text-align: center;
		color: #cd1e03;
		text-shadow: 1px 1px 3px #ffd728;
	}

	@-webkit-keyframes pic-rotate {
		0% {
			-webkit-transform: rotate(0deg);
		}

		100% {
			-webkit-transform: rotate(360deg);
		}
	}

	@-webkit-keyframes pic-shake {
		0% {
			-webkit-transform: scale(1);
		}

		10%,
		20% {
			-webkit-transform: scale(0.9) rotate(-3deg);
		}

		30%,
		50%,
		70%,
		90% {
			-webkit-transform: scale(1.1) rotate(3deg);
		}

		40%,
		60%,
		80% {
			-webkit-transform: scale(1.1) rotate(-3deg);
		}

		100% {
			-webkit-transform: scale(1) rotate(0);
		}
	}
</style>