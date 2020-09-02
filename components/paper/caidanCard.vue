<template>
	<view>
		<!-- 菜单选项卡 -->
		<view class="caidan_wrapper animate__animated animate__fadeInRight" v-if="isShowCaidan">
			<view hover-class="active" @click="addFriends">
				<view class="icon iconfont icon-sousuo"></view> 加糗友
			</view>
			<view hover-class="active" @click="clearAll">
				<view class="icon iconfont icon-qingchu"></view> 清除未读
			</view>
		</view>
		<!-- 遮罩层 -->
		<view class="zhezhaoceng" v-if="isShowCaidan" @click="hideCaidan"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:['isShowCaidan'],
		methods:{
			addFriends(){
				this.$emit("addFriends")
			},
			clearAll(){
				this.$emit("clearAll")
			},
			hideCaidan(){
				this.$emit("hideCaidan")
			}
		}
	}
</script>

<style lang="less">
	.caidan_wrapper{
		position: fixed;
		right: 0;
		// #ifdef H5
		top: 90rpx;
		// #endif
		// #ifdef APP-PLUS
		top: var(--status-bar-height);
		// #endif
		width: 400rpx;
		z-index: 999;
		background-color: #fff;
		box-shadow: 0 0 10rpx 0 hsla(0,0%,0%,.2);
		view{
			display: flex;
			align-items: center;
			padding: 15rpx 20rpx;
		}
	}
	.zhezhaoceng{
		position: fixed;
		content: '';
		left: 0;
		top: 0;
		right: 0;
		bottom: 0;
		z-index: 998;
	}
</style>
