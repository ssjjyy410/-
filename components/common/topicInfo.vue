<template>
	<view class="detail_header">
		<view class="bg">
			<image :src="topicInfo.topicpic" mode="aspectFill"></image>
		</view>
		<view class="topic">
			<view class="topic_pic">
				<image :src="topicInfo.topicpic" mode="aspectFill"></image>
			</view>
			<view class="topic_title">{{topicInfo.topictitle}}</view>
		</view>
		<view class="dynamic">动态 {{topicInfo.dynamicnum}} 今日 {{topicInfo.todaynum}}</view>
		<view class="desc">{{topicInfo.desc}}</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:["topicInfo"]
	}
</script>

<style lang="less" scoped>
	.detail_header{
		width: 100%;
		.bg{
			position: relative;
			width: 100%;
			height: 300rpx;
			overflow: hidden;
			image{
				filter: blur(10rpx);
				width: 100%;
				height: 100%;
			}
		}
		.topic{
			width: 100%;
			min-height: 100rpx;
			position: relative;
			.topic_pic{
				position: absolute;
				width: 150rpx;
				height: 150rpx;
				border-radius: 20rpx;
				overflow: hidden;
				left: 20rpx;
				top: -75%;
				image{
					width: 100%;
					height: 100%;
				}
			}
			.topic_title{
				height: 100%;
				word-break: break-all;
				text-overflow: ellipsis;
				overflow: hidden;
				position: absolute;
				left: 180rpx;
				padding-right: 20rpx;
			}
		}
		.dynamic,.desc{
			color: #a3a3a3;
			font-size: 35rpx;
			margin: 10rpx 20rpx;
		}
		.dynamic{
			font-size: 30rpx;
			color: #cecece;
		}
	}
</style>
