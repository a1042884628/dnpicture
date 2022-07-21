<template>
	<scroll-view scroll-y enable-flex class="video_category" @scrolltolower="handleScrolltolower"> 
		<view class="video_item" v-for="item in videowp" :key="item.id">
			<image mode="widthFix" :src="item.cover"></image>
			<view class="cate_name">{{item.name}}</view>
		</view>
	</scroll-view>
</template>

<script>
	export default {
		data() {
			return {
				videowp: []
				// hasMore:true
			}
		},
		mounted() { /* 挂载组件的时候触发mounted*/
			// 修改页面的标题
			uni.setNavigationBarTitle({
				title: "分类"
			});
			this.getList();
		},
		methods: {
			getList() {
				this.request({
					url: "http://service.picasso.adesk.com/v1/vertical/category"
				}).then(result => {
					// console.log(result)
					this.videowp=result.res.category;
					// console.log(this.videowp)
				})
			},
			// 分页事件
			handleScrolltolower() {
				if (this.hasMore) {
					this.urlobj.params.skip += this.urlobj.params.limit;
					this.getList();
				} else {
					uni.showToast({
						title: "没有更多数据了",
						icon: "none"
					})
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.video_category {
		display: flex;
		flex-wrap: wrap;
		// height: calc(100vh - 36px);

		.video_item {
			width: 33.33%;
			position: relative;
			border: 5rpx solid #fff;
			
			image {
				height: 100%;
			}
			.cate_name {
				position: absolute;
				width: 100%;
				height: 50rpx;
				left: 0;
				bottom: 0;
				color: #fff;
				// css3 渐变
				background-image: linear-gradient(to right top, rgba(0, 0, 0, .2), rgba(0, 0, 0, 0));
				font-size: 40rpx;
				display: flex;
				align-items: center;
				padding-left: 20rpx;
			}
		}
	}
</style>
