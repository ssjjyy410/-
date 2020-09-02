<template>
	<scroll-view class="nav_wrapper" scroll-x scroll-with-animation :scroll-into-view="tabBars[tabIndex].id">
		<view 
			class="nav_item" 
			 :style="tabStyle"
			:id="item.id"
			:class="{'active':tabIndex===index}" 
			v-for="(item,index) in tabBars" 
			:key="item.id"
			@click="tabTap(index)"
		>{{item.name}} {{item.num?item.num:''}}</view>
	</scroll-view>
</template>

<script>
	export default {
		data() {
			return {
			};
		},
		props:['tabBars',"tabIndex","tabStyle"],
		methods:{
			tabTap(index){
				this.$emit('tabTap',index)
			}
		}
	}
</script>

<style lang="less" scoped>
	.nav_wrapper{
		white-space: nowrap;
		width: 100%;
		line-height: 80rpx;
		font-size: 35rpx;
		.nav_item{
			position: relative;
			display: inline-block;
			width: 140rpx;
			text-align: center;
			color: #979797;
		}
	}
	.active{
		&::before{
			content: '';
			position: absolute;
			top: 70%;
			left: 50%;
			bottom: 17%;
			transform: translateX(-50%);
			width: 70rpx;
			background-color: #fede33;
			border-radius: 5rpx;
		}
		color: #000 !important;
	}
</style>
