<template>
	<view @click="handleClick">
		<slot></slot>
	</view>
</template>

<script>
	export default {
		props: {
			// 接受父组件传过来的数据
			list: Array,
			index: Number
		},
		methods:{
			handleClick(){
				//  1. 将数据缓存下来  实现数据共享
				getApp().globalData.imgList=this.list;
				getApp().globalData.imgIndex=this.index;
				//  2. 再实现点击跳转页面  通过JSON的方式跳转
				uni.navigateTo({
					url:"/pages/imgDetail/index"
				})
			}
		}
	}
</script>

<style>
</style>
