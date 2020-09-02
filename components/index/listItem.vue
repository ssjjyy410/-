<template>
	<view class="u_list_item animate__animated animate__bounceInUp">
		<view class="item_header">
			<view class="header_left">
				<image :src="item.userpic" mode="aspectFill" lazy-load></image>
				{{item.username}}
			</view>
			<view class="header_right">
				<view class="guanzhu" :class="{'icon iconfont icon-zengjia':item.isguanzhu}" @click="toggleGuanzhu">{{item.isguanzhu?'关注':'已关注'}}</view>
				<view class="close icon iconfont icon-guanbi" @click="closeItem"></view>
			</view>
		</view>
		<view class="title" @click="jumpToDetail">{{item.title}}</view>
		<view class="media" @click="jumpToDetail">
			<image :src="item.titlepic" mode="widthFix" lazy-load></image>
			<template v-if="isVideo">
				<view class="icon iconfont icon-bofang"></view>
				<view class="video_jilu">
					{{item.video.looknum}}<view class="txt">次播放</view>{{item.video.long}}
				</view>
			</template>
		</view>
		<view class="footer">
			<view class="footer_left">
				<view @click="dingTap" class="icon iconfont icon-icon_xiaolian-mian" :class="{'active':item.infonum.index===1}"></view>
				<view @click="dingTap" class="xiaolian_num">
					{{item.infonum.dingnum}}
				</view>
				<view @click="caiTap" class="icon iconfont icon-kulian" :class="{'active':item.infonum.index===2}"></view>
				<view @click="caiTap" class="kulian_num">
					{{item.infonum.cainum}}
				</view>
			</view>
			<view class="footer_right">
				<view class="icon iconfont icon-pinglun1"></view>
				<view class="pinglun1_num">
					{{item.commentnum}}
				</view>
				<view class="icon iconfont icon-zhuanfa"></view>
				<view class="zhuanfa_num">
					{{item.sharenum}}
				</view>
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
		props:["item","index","index1"],
		computed:{
			isVideo:function(){
				return this.item.type==='video'
			}
		},
		methods:{
			//关注或取消关注
			toggleGuanzhu(){
				this.item.isguanzhu=!this.item.isguanzhu
				uni.showToast({
					title:"成功"
				})
			},
			//顶
			dingTap(){
				let index=this.item.infonum.index
				switch(index){
					case 0:
						this.item.infonum.dingnum++;
						this.item.infonum.index=1;
						break;
					case 1:
						break;
					case 2:
						this.item.infonum.dingnum++;
						this.item.infonum.cainum--;
						this.item.infonum.index=1;
						break;
				}
			},
			//踩
			caiTap(){
				let index=this.item.infonum.index
				switch(index){
					case 0:
						this.item.infonum.cainum++;
						this.item.infonum.index=2;
						break;
					case 1:
						this.item.infonum.cainum++;
						this.item.infonum.dingnum--;
						this.item.infonum.index=2;
						break;
					case 2:
						break;
				}
			},
			//关闭该项
			closeItem(){
				this.$emit("closeItem",{"index":this.index,"index1":this.index1})
			},
			jumpToDetail(){
				let that=this;
				uni.navigateTo({
					url:"/pages/detail/detail?itemDetail="+JSON.stringify(this.item)
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.u_list_item{
		box-sizing: border-box;
		width: 750rpx;
		padding: 20rpx;
		border-bottom: 1px solid #eee;
		.item_header{
			display: flex;
			align-items: center;
			width: 100%;
			.header_left{
				width: 100%;
				font-size: 30rpx;
				color: #a4a4a4;
				image{
					width: 80rpx;
					height: 80rpx;
					border-radius: 50%;
					vertical-align: middle;
					margin-right: 10rpx;
				}
			}
			.header_right{
				display: flex;
				align-items: center;
				.guanzhu{
					text-align: center;
					font-size: 25rpx;
					background-color: #f4f4f4;
					display: inline-block;
					width: 100rpx;
					line-height: 40rpx;
					border-radius: 2rpx;
				}
				.close {
					font-size: 25rpx;
					margin-left: 20rpx;
					color: #d6d6d6;
				}
			}
		}
		.title{
			word-wrap: break-word;
			margin: 20rpx 0;
		}
		.media{
			width: 100%;
			margin-bottom: 40rpx;
			position: relative;
			image{
				width: 100%;
				border-radius: 20rpx;
			}
			.icon-bofang{
				position: absolute;
				color: #fff;
				font-size: 150rpx;
				left: 50%;
				top: 50%;
				transform: translate(-50%,-50%);
			}
			.video_jilu{
				box-sizing: border-box;
				position: absolute;
				display: flex;
				right: 10rpx;
				bottom: 20rpx;
				padding: 10rpx 20rpx;
				border-radius: 30rpx;
				color: #fff;
				font-size: 25rpx;
				background-color: hsla(0,0%,0%,.6);
				.txt{
					margin: 0 10rpx;
				}
			}
		}
		.footer{
			box-sizing: border-box;
			width: 100%;
			padding: 0 10rpx;
			margin-bottom: 20rpx;
			display: flex;
			justify-content: space-between;
			align-items: center;
			color: #d5d5d5;
			.footer_left,.footer_right{
				display: flex;
				align-items: center;
				.icon-icon_xiaolian-mian,.icon-kulian,.icon-pinglun1,.icon-zhuanfa{
					margin-right: 10rpx;
				}
				.xiaolian_num,.kulian_num,.pinglun1_num,.zhuanfa_num{
					margin-right: 10rpx;
				}
			}
		}
	}
	.active,.active+view{
		color: #fede33;
	}
</style>
