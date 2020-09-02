<template>
	<view class="func_wrapper">
		<view 
			class="func_item" 
			hover-class="active" 
			v-for="(item,index) in list" 
			:key="index" 
			v-if="isLogin||item.name!=='审核糗事'"
			@click="jumpToPath(item)"
		>
			<view class="left">
				<view :class="`icon iconfont ${item.icon}`" v-if="item.icon"></view>
				<view class="title">{{item.name}}</view>
			</view>
			<view class="right icon iconfont icon-jinru"></view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:["list","isLogin"],
		methods:{
			//跳转
			jumpToPath(item){
				switch(item.jumpType){
					case "navigateTo":
						console.log(item.path)
						uni.navigateTo({
							url: item.path
						});
						break;
					case "switchTab":
						uni.switchTab({
							url:item.path
						});
						break;
					default:
						break;
				}
			}
		}
	}
</script>

<style lang="less" scoped>
	.func_wrapper{
		width: 100%;
		.func_item{
			box-sizing: border-box;
			display: flex;
			justify-content: space-between;
			align-items: center;
			width: 100%;
			padding: 30rpx;
			border-bottom: 1rpx solid #eee;
			.left{
				font-size: 40rpx;
				.icon{
					font-size: 42rpx;
					width: 50rpx;
					text-align: center;
					color: #45b3ff;
					display: inline-block;
					margin-right: 20rpx;
				}
				.icon-huiyuanvip{font-size: 38rpx;color: #ff7434;}
				.icon-guanyuwomen{font-size: 34rpx;}
				.title{
					font-size: 35rpx;
					display: inline-block;
				}
			}
			.right{color: #bcbcbc;}
		}
	}
	.active{
		background-color: #eee;
	}
</style>
