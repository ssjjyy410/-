<template>
	<view class="paper_list" @click="jumpToUserChat">
		<image class="image" :src="paperInfo.userpic" mode="aspectFill" lazy-load></image>
		<view class="info">
			<view class="head">
				<view class="user">{{paperInfo.username}}<view>{{paperInfo.time}}</view></view>
				<view class="con"><view class="txt">{{paperInfo.desc}}</view><uni-badge :text="paperInfo.noreadnum" type="error"></uni-badge></view>
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
		props:["paperInfo"],
		methods:{
			jumpToUserChat(){
				uni.navigateTo({
					url:"/pages/userChat/userChat"
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.paper_list{
		display: flex;
		box-sizing: border-box;
		margin: 20rpx;
		padding-bottom: 20rpx;
		border-bottom: 1rpx solid #eee;
		.image{
			width: 20%;
			height: 120rpx;
			border-radius: 50%;
		}
		.info{
			width: 80%;
			margin-left: 20rpx;
			.user{
				display: flex;
				justify-content: space-between;
				align-items: center;
				view{
					font-size: 27rpx;
					color: #cbcbcb;
				}
			}
			.con{
				width: 100%;
				margin-top: 10rpx;
				display: flex;
				justify-content: space-between;
				.txt{
					width: 100%;
					font-size: 30rpx;
					color: #9c9c9c;
					text-overflow: ellipsis;
					overflow: hidden;
					white-space: nowrap;
				}
			}
		}
	}
</style>
