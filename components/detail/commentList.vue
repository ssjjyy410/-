<template>
	<view class="comment_list animate__animated animate__fadeInUp">
		<image :src="list.userpic" mode="aspectFill" lazy-load></image>
		<view class="comment">
			<view class="username">{{list.username}}</view>
			<view class="title">{{list.fid===1?`回复 ${list.replytoUser.username} : `:''}}{{list.data}}</view>
			<view class="footer">
				<view class="day">{{transTime}}</view>
				<view 
					class="pinglun" 
					@click="isShowReply"
					v-if="list.fid===0"
				>{{list.reply.length>0?list.reply.length:''}}回复</view>
			</view>
		</view>
	</view>
</template>

<script>
	import time from '../../common/time.js'
	
	export default {
		data() {
			return {
				
			};
		},
		props:["list"],
		computed:{
			//转换时间
			transTime(){
				return time.gettime.gettime(this.list.time)
			}
		},
		methods:{
			//是否显示回复
			isShowReply(){
				this.$emit("isShowReply")
			},
			
		}
	}
</script>

<style lang="less" scoped>
	.comment_list{
		display: flex;
		margin: 20rpx 0;
		image{
			width: 80rpx;
			height: 80rpx;
			border-radius: 50%;
		}
		.comment{
			flex: 1;
			margin-left: 20rpx;
			.username{
				font-size: 35rpx;
				color: #159dd7;
			}
			.title{
				margin: 20rpx 0;
				font-size: 37rpx;
				word-break: break-all;
				overflow: hidden;
			}
			.footer{
				display: flex;
				justify-content: space-between;
				align-items: center;
				font-size: 28rpx;
				.day{
					color: #cdcdcd;
				}
				.pinglun{
					border-radius: 20rpx;
					padding: 5rpx 10rpx;
					background-color: #eee;
					color: #777;
				}
			}
		}
	}
</style>
