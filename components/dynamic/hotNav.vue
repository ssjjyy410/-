<template>
	<view class="hot_wrapper">
		<view class="hot_header">
			<view class="hot_title">热门分类</view>
			<view class="hot_more" @click="jumpTo">更多 ></view>
		</view>
		<view class="hot_item">
			<view v-for="(item,index) in hotNavs" :key="index">{{item.name}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:['hotNavs'],
		methods:{
			jumpTo(){
				this.$emit("jumpTo")
			}
		}
	}
</script>

<style lang="less" scoped>
	.hot_wrapper{
		margin: 20rpx 20rpx 0;
		font-size: 35rpx;
		.hot_header{
			display: flex;
			justify-content: space-between;
			.hot_more{
				color: #d9d9d9;
			}
		}
		.hot_item{
			display: flex;
			justify-content: space-evenly;
			align-items: center;
			padding: 20rpx 10rpx 30rpx;
			border-bottom: 1px solid #eee;
			view{
				color: #9f9f9f;
				background-color: #f7f7f7;
				font-size: 30rpx;
				flex: 1;
				margin: 0 8rpx;
				padding: 10rpx 5rpx;
				text-align: center;
			}
		}
	}
</style>
