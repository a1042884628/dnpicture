<!-- 
  1. slot
	2. 对外提供数据 滑动方向
 -->
<template>
	<view @touchstart="handeTouchstart" @touchend="handeTouchend">
		<slot></slot>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 按下的时间
				startTime: 0,
				// 按下的坐标
				startX: 0,
				startY: 0
			}

		},
		methods: {
			// 用户按下屏幕 
			handeTouchstart(event) {
				// console.log("手指按下屏幕");
				// console.log("按下:" + event.changedTouches[0].clientX);
				// console.log("按下:" + event.changedTouches[0].clientY);

				this.startTime = Date.now();
				this.startX = event.changedTouches[0].clientX;
				this.startY = event.changedTouches[0].clientY;
			},
			handeTouchend(event) {
				// console.log("手指离开屏幕");
				// console.log("离开:" + event.changedTouches[0].clientX);
				// console.log("离开:" + event.changedTouches[0].clientY);

				const endTime = Date.now();
				const endX = event.changedTouches[0].clientX;
				const endY = event.changedTouches[0].clientY;

				// 判断按下的时长 是否大于2000
				if (endTime - this.startTime > 2000) {
					return;
				}

				// 滑动的方向 
				let direction = "";

				// 判断用户滑动的距离 是否合法  合法: 再去判断滑动的方向  注意: 距离加上绝对值
				if (Math.abs(endX - this.startX) > 10&&Math.abs(endY-this.startY<10)) {
					// 判断滑动方向
					direction = endX - this.startX > 0 ? "right" : "left";
				} else {
					return;
				}

				// 进行到这,表明用户做了一个合法的操作
				// console.log(direction);
				// 向父组件传递数据
				this.$emit("swiperAction",{direction});
			}
		}
	};
</script>

<style>
</style>
