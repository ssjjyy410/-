<template>
	<view class="user_list animate__animated animate__bounceInUp">
		<view class="userpic">
			<image :src="item.userpic" mode="aspectFill"></image>
		</view>
		<view class="userinfo">
			<view class="nameandsex">
				<view class="username">{{item.username}}</view>
				<user-sex :sex="item.sex" :age="item.age"/>
			</view>
			<view class="icon iconfont" :class="item.isGuanzhu?'icon-xuanze-yixuan':'icon-zengjia1'" @click="toggleGuanzhu"></view>
		</view>
	</view>
</template>

<script>
	import userSex from '../../components/common/userSex.vue'
	
	export default {
		data() {
			return {
				
			};
		},
		props:["item","index"],
		components:{
			userSex
		},
		methods:{
			toggleGuanzhu(){
				this.$emit("toggleGuanzhu",this.index)
			}
		}
	}
</script>

<style lang="less">
	.user_list{
		display: flex;
		justify-content: space-between;
		box-sizing: border-box;
		margin: 20rpx;
		padding: 20rpx 0 30rpx;
		border-bottom: 1rpx solid #eee;
		.userpic{
			width: 150rpx;
			height: 150rpx;
			overflow: hidden;
			border-radius: 50%;
			image{
				width: 100%;
				height: 100%;
			}
		}
		.userinfo{
			flex: 1;
			margin-left: 30rpx;
			display: flex;
			justify-content: space-between;
			align-items: center;
			.nameandsex{
				.username{
					margin-bottom: 20rpx;
				}
			}
			.icon-xuanze-yixuan{
				color: #ccc;
			}
			.icon-zengjia1{
				color: #f8791c;
			}
		}
	}
</style>
