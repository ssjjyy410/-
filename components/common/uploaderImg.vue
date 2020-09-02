<template>
	<view class="ci_wrapper">
		<view class="ci_header">
			<view>点击可预览选择好的图片</view>
			<view class="shuliang">{{tempFilePaths.length}}/{{count}}</view>
		</view>
		<view class="ci_img">
			<view 
				class="ci_choosed_img" 
				@click="previewImg(index)"
				v-for="(url,index) in tempFilePaths"
				:key="index"
			>
				<view 
					class="shanchu icon iconfont icon-shanchu"
					@click.stop="shanchuImg(index)"
				></view>
				<image
					:src="url"
					mode="aspectFill"
				></image>
			</view>
			<view class="ci_choose" @click="chooseImg">+</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				tempFilePaths:[],//图片的本地文件路径列表
				tempFiles:[] //图片的本地文件列表，每一项是一个 File 对象
			};
		},
		props:["count"],
		methods:{
			//选择图片
			chooseImg(){
				let that=this;
				uni.chooseImage({
					count:that.count,
					success: (res) => {
						that.tempFilePaths=[...that.tempFilePaths,...res.tempFilePaths]
						that.tempFiles=[...that.tempFiles,...res.tempFiles]
						// console.log(that.tempFilePaths,that.tempFiles)
						this.chooseUrlAndName()
					}
				})
			},
			//预览图片
			previewImg(index){
				let that=this;
				uni.previewImage({
					current:index,
					urls: that.tempFilePaths,
					indicator: "number",
					loop: true
				})
			},
			//删除图片
			shanchuImg(index){
				this.tempFilePaths.splice(index,1)
				this.tempFiles.splice(index,1)
				this.chooseUrlAndName()
			},
			//筛选并发送图片
			chooseUrlAndName(){
				let arr=[],
					tempFiles=this.tempFiles
				tempFiles.forEach(item=>{
					arr.push({
						name: item.name,
						path: item.path
					})
				})
				this.$emit("uploadImg",arr)
			}
		}
	}
</script>

<style lang="less" scoped>
	.ci_wrapper{
		margin: 20rpx;
		.ci_header{
			display: flex;
			justify-content: space-between;
			font-size: 30rpx;
			.shuliang{
				color: #b2b2b2;
			}
		}
		.ci_img{
			margin-top: 20rpx;
			.ci_choose{
				display: inline-block;
				margin-right: 10rpx;
				margin-top: 20rpx;
				width: 220rpx;
				line-height: 220rpx;
				text-align: center;
				color: #d9d9d9;
				font-size:290rpx;
				font-weight: lighter;
				background-color: #f5f5f5;
				border-radius: 10rpx;
			}
			.ci_choosed_img{
				position: relative;
				display: inline-block;
				margin-right: 10rpx;
				margin-top: 20rpx;
				width: 220rpx;
				height: 220rpx;
				border-radius: 10rpx;
				border: 1rpx solid hsla(0,0%,0%,.1);
				overflow: hidden;
				.shanchu{
					position: absolute;
					right: 5rpx;
					top: 5rpx;
					font-size: 30rpx;
					background-color: hsla(0,0%,0%,.5);
					color: #fff;
					z-index: 999;
				}
				image{
					width: 100%;
					height: 100%;
				}
			}
		}
	}
</style>
