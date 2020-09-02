<template>
	<view class="zuijin_item animate__animated animate__fadeInLeft" @click="jumpToTopicDetail">
		<view class="image">
			<image :src="list.titlepic" mode="aspectFill"></image>
		</view>
		<view class="zuijin_con">
			<view class="title">{{list.title}}</view>
			<view class="con">{{list.dec}}</view>
			<view class="footer">动态 {{list.totalnum}} 今日 {{list.todaynum}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:['list'],
		methods:{
			jumpToTopicDetail(){
				uni.navigateTo({
					url: '/pages/topicDetail/topicDetail'
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.zuijin_item{
		margin: 20rpx 0 0 0;
		padding-bottom: 30rpx;
		box-sizing: border-box;
		display: flex;
		border-bottom: 1rpx solid #eee;
		.image{
			width: 200rpx;
			height: 200rpx;
			overflow: hidden;
			border-radius: 20rpx;
			image{
				width: 100%;
				height: 100%;
			}
		}
		.zuijin_con{
			margin-left: 20rpx;
			flex: 1;
			.con,.title,.footer{
				word-break: break-all;
				margin-bottom: 15rpx;
			}
			.con,.footer{
				color: #a4a4a4;
				font-size: 30rpx;
			}
		}
	}
</style>
