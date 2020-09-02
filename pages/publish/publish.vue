<template>
	<view>
		<uni-nav-bar
			left-icon="back" 
			right-text="发布" 
			status-bar
			@clickLeft="goBack"
			@clickRight="publishMine"
		>
			<view class="juzhong" @click="showSheet">
				{{yinsi}}
				<view class="icon iconfont icon-xialazhankai"></view>
			</view>
		</uni-nav-bar>
		<view class="text_wrapper">
			<textarea :value="text" placeholder="说一句话吧~" @blur="setText"/>
		</view>
		<uploader-img :count="6" @uploadImg="uploadImg"/>
		<uni-popup class="popUp" ref="popup">
			<view class="tip">
				<image src="../../static/common/addinput.png" mode="widthFix"></image>
				<view class="list">
					1、涉及黄色,政治,广告及骚扰信息
				</view>
				<view class="list">
					2、涉及人身攻击
				</view>
				<view class="list">
					3、留联系方式,透露他人隐私
				</view>
				<view class="list">
					一经核实将被封禁,情节严重者永久封禁
				</view>
				<button class="btn" type="default" @click="closePopUp">朕知道了</button>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue"
	import uploaderImg from '../../components/common/uploaderImg.vue'
	import uniPopup from '../../components/uni-popup/uni-popup.vue'
	import base64 from "../../common/base64.js";
	
	export default {
		data() {
			return {
				yinsiArr:["所有人可见","仅自己可见"],
				yinsi:"所有人可见",
				text:"",//文本内容
				tempFiles:[],//图片信息
				isSaveText: false //是否保存草稿
			};
		},
		components:{
			uniNavBar,
			uploaderImg,
			uniPopup
		},
		methods:{
			//返回
			goBack(){
				let that=this;
				//无内容
				if(that.text===""&&that.tempFiles.length<=0){
					uni.navigateBack({
						delta:1
					});
					return;
				};
				//有内容
				uni.showModal({
				    title: '警告',
				    content: '退出前是否保存内容为草稿?',
				    success: function (res) {
				        if (res.confirm) {
				            //保存
							that.isSaveText=true;
							let obj={
									"text":that.text,
									"tempFiles": that.tempFiles,
									"yinsi":that.yinsi
								};
							let b64=base64.Base64;
							uni.setStorage({
							    key: `Caogao${new Date().getTime()}`,
							    data: b64.encode(JSON.stringify(obj)),
							    success: function () {
							        uni.showToast({
							        	title:"保存成功"
							        })
							    }
							});
				        }
						uni.navigateBack({
							delta:1
						})
				    }
				});
			},
			//发布
			publishMine(){
				console.log("发布")
			},
			//隐私
			showSheet(){
				let that=this
				uni.showActionSheet({
				    itemList: that.yinsiArr,
				    success: function (res) {
						that.yinsi=that.yinsiArr[res.tapIndex]
				    }
				});
			},
			//上传图片
			uploadImg(tempFiles){
				console.log(tempFiles)
				this.tempFiles=tempFiles
			},
			//关闭提示框
			closePopUp(){
				this.$refs.popup.close()
			},
			// 输入框设置值
			setText(e){
				this.text=e.detail.value
			}
		},
		onReady(){
			this.$refs.popup.open()
		}
	}
</script>

<style lang="less" scoped>
	.juzhong{
		margin: 0 auto;
		display: flex;
	}
	.text_wrapper{
		width: 100%;
		height: 400rpx;
		border-bottom: 1rpx solid hsla(0,0%,0%,.05);
		textarea{
			box-sizing: border-box;
			padding: 20rpx;
			width: 100%;
		}
	}
	.popUp{
		.tip{
			box-sizing: border-box;
			display: flex;
			flex-direction: column;
			background-color: #fff;
			padding: 20rpx 40rpx;
			width: 500rpx;
			border-radius: 10rpx;
			image{
				align-self: center;
				width: 60%;
				margin-bottom: 10rpx;
			}
			.list{
				box-sizing: border-box;
				padding: 10rpx 0;
				align-self: flex-start;
				font-size: 28rpx;
			}
			.btn{
				font-size: 30rpx;
				color: #000;
				background-color: #ffe934;
				width: 100%;
			}
		}
	}
</style>
