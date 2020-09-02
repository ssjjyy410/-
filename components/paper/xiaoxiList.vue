<template>
	<view>
		<view class="time" v-if="xiaoxi.gsTime">{{xiaoxi.gsTime}}</view>
		<view :class="xiaoxi.isme?'myxiaoxi jiantou_left':'other jiantou_right'">
			<image class="userpic" :src="xiaoxi.userpic" mode="aspectFill"></image>
			<!-- 文字 -->
			<view class="xiaoxi" v-if="xiaoxi.type==='text'">{{xiaoxi.data}}</view>
			<!-- 图片 -->
			<view class="xiaoxi" v-else>
				<image :src="xiaoxi.data" mode="widthFix"></image>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:["xiaoxi","index"]
	}
</script>

<style lang="less" scoped>
	.time{
		width: 100%;
		text-align: center;
		font-size: 25rpx;
		color: #a2a2a2;
	}
	.myxiaoxi,.other{
		display: flex;
		margin: 40rpx 0 80rpx;
		.userpic{
			width: 100rpx;
			height: 100rpx;
			border-radius: 50%;
		}
		.xiaoxi{
			position: relative;
			box-sizing: border-box;
			font-size: 35rpx;
			border-radius: 20rpx;
			width: 350rpx;
			padding: 20rpx 30rpx 10rpx;
			margin-left: 20rpx;
			background-color: #f4f4f4;
			image{
				width: 100%;
			}
		}
	}
	.other{
		flex-direction: row-reverse;
		.xiaoxi{
			margin-right: 20rpx;
		}
	}
	.jiantou_left{
		.xiaoxi::before{
			position: absolute;
			content: "";
			left: -60rpx;
			top: 10rpx;
			width: 0;
			border: 40rpx solid #f4f4f4;
			border-color: transparent #f4f4f4 transparent transparent;
		}
	}
	.jiantou_right{
		.xiaoxi::before{
			position: absolute;
			content: "";
			right: -60rpx;
			top: 10rpx;
			width: 0;
			border: 40rpx solid #f4f4f4;
			border-color: transparent transparent transparent #f4f4f4;
		}
	}
</style>
