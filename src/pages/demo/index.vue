<template>
	<view @touchstart="handeTouchstart" @touchend="handeTouchend">学习触屏事件</view>
</template>

<script>
	/* 
	  1. 给容器绑定两个触屏事件 touchstart和touchend
    2. 用户按下屏幕事件
			1. 记录用户按下屏幕的时间 Date.now() 时间戳  1970 -1-1到现在的毫秒数
			2. 记录用户按下屏幕的坐标 x 和 y
		3. 用户离开屏幕事件
			1. 记录用户离开屏幕的时间 Date.now()
			2. 记录用户离开屏幕的坐标 x 和 y
			3. 根据两个时间 做运算 判断 用户按下的时长是否合法
			4. 根据两对坐标 判断距离是否合法   合法后再判断滑动的方向
	 */
	export default {
		data() {
			return {
				// 按下的时间
				startTime:0,
				// 按下的坐标
				startX:0,
				startY:0
			}

		},
		methods: {
			// 用户按下屏幕 
			handeTouchstart(event) {
				// console.log("手指按下屏幕");
				// console.log("按下:" + event.changedTouches[0].clientX);
				// console.log("按下:" + event.changedTouches[0].clientY);
				
				this.startTime=Date.now();
				this.startX=event.changedTouches[0].clientX;
				this.startY=event.changedTouches[0].clientY;
			},
			handeTouchend(event) {
				// console.log("手指离开屏幕");
				// console.log("离开:" + event.changedTouches[0].clientX);
				// console.log("离开:" + event.changedTouches[0].clientY);
				
				const endTime=Date.now();
				const endX=event.changedTouches[0].clientX;
				const endY=event.changedTouches[0].clientY;
				
				// 判断按下的时长
				if(endTime-this.startTime>2000){
					return;
				}
				
				// 滑动的方向 
				let direction="";
				
				// 判断用户滑动的距离 是否合法  合法: 再去判断滑动的方向  注意: 距离加上绝对值
				if(Math.abs(endX-this.startX)>10){
					// 判断滑动方向
					direction=endX-this.startX>0?"right":"left";
				}else{
					return;
				}
				
				// 进行到这,表明用户做了一个合法的操作
				console.log(direction);
			}
		}
	}
</script>

<style>
	view {
		width: 100%;
		height: 500rpx;
		background-color: aqua;
	}
</style>
