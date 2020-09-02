<template>
	<view class="login_wrapper">
		<image class="login_userpic" :src="mineinfo.userpic" mode="aspectFill"></image>
		<view class="login_userinfo">
			<view class="login_user">
				<view class="login_username">{{mineinfo.username}}</view>
				<view class="login_data">总访客 {{mineinfo.totalnum}} 今日 {{mineinfo.todaynum}}</view>
			</view>
			<view class="icon iconfont icon-jinru"></view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:["mineinfo"]
	}
</script>

<style lang="less" scoped>
	.login_wrapper{
		box-sizing: border-box;
		display: flex;
		margin: 20rpx 0 30rpx;
		.login_userpic{
			width: 120rpx;
			height: 120rpx;
			border-radius: 50%;
		}
		.login_userinfo{
			flex: 1;
			margin-left: 20rpx;
			display: flex;
			justify-content: space-between;
			align-items: center;
			.login_user{
				.login_data{
					margin-top: 10rpx;
					font-size: 30rpx;
					color: #989898;
				}
			}
		}
	}
	
</style>
