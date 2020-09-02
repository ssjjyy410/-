<template>
	<uni-nav-bar
		class="navbar"
		status-bar
	>
		<view slot="left" class="left icon iconfont" :class="left" @click="handleLeftClick"></view>
		<view class="juzhong">
			<view :class="{'active':navIndex===index}" v-for="(item,index) in navBars" :key="item.id" @click="toggleNav(index)">{{item.name}}</view>
		</view>
		<view slot="right" class="right icon iconfont" :class="right" @click="handleRightClick"></view>
	</uni-nav-bar>
</template>

<script>
	import uniNavBar from '../uni-nav-bar/uni-nav-bar.vue'
	export default {
		data() {
			return {
				
			};
		},
		props:['navBars','navIndex','left','right'],
		components:{
			uniNavBar
		},
		methods:{
			//导航栏切换
			toggleNav(index){
				this.$emit("toggleNav",index)
			},
			//右边按钮
			handleRightClick(){
				this.$emit("handleRightClick")
			},
			//左边按钮
			handleLeftClick(){
				this.$emit("handleLeftClick")
			},
		}
	}
</script>

<style lang="less">
	.navbar{
		position: fixed;
		z-index: 999;
		.juzhong{
				margin: 0 auto;
				display: flex;
				view{
					margin-right: 20rpx;
				}
		}
		.right{
			margin-right: -70rpx;
		}
		.icon-qiandao{
			color: #ff9619;
		}
		.right,.left{
			font-size: 40rpx;
		}
	}
	.active{
		position: relative;
		&::before{
			content: '';
			position: absolute;
			top: 70%;
			bottom: 18%;
			left: -5rpx;
			right: -5rpx;
			background-color: #fede33;
			border-radius: 5rpx;
		}
		color: #000 !important;
	}
</style>
