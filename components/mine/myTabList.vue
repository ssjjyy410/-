<template>
	<view class="list_wrapper">
		<view class="list_item" v-for="(item,index) in minedata" :key="index">
			{{item.num}}<view class="itemname">{{item.name}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:["minedata"]
	}
</script>

<style lang="less" scoped>
	.list_wrapper{
		width: 100%;
		display: flex;
		margin-bottom: 30rpx;
		.list_item{
			flex: 1;
			margin: 0 20rpx;
			text-align: center;
			font-size: 35rpx;
			
			.itemname{
				font-size: 32rpx;
				color: #989898;
			}
		}
	}
	
</style>
