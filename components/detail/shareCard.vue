<template>
	<view v-if="isShowFenxiang">
		<view class="share_zhezhao" @click="hideFenxiang"></view>
		<view class="share_wrapper animate__animated animate__fadeInUp animate__faster">
			<view class="share_title">分享到</view>
			<scroll-view scroll-x class="share_list">
				<view 
					class="share_item" 
					hover-class="active"
					v-for="(item,index) in provider"
					:key="index"
					@click="share(item)"
				>
					<view class="share_img icon iconfont" :class="item.zicon"></view>
					<view class="share_desc">{{item.name}}</view>
				</view>
			</scroll-view>
			<view class="share_cancel" @click="hideFenxiang">取消</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				provider:[],//支持分享的服务商
				shareData:{
					shareText:"你喜欢的都在这里,快来看看吧!",
					href:"https://uniapp.dcloud.io",
					image:"https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
					shareType:1//0图文 1文字 2图片
				},
			};
		},
		props:["isShowFenxiang","list"],
		methods:{
			//隐藏面板
			hideFenxiang(){
				this.$emit("hideFenxiang")
			},
			//分享
			async share(e){
				let shareData=this.shareData
				let list=this.list
				// 分享的内容即为详情中的内容
				this.shareData.shareText=`${shareData.shareText} ${list.title}`;
				// 如果图片存在的话就设置图片链接
				this.image=list.titlepic?list.titlepic:"https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png";
				//如果分享内容为空
				if(!shareData.shareText&&(shareData.shareType===0||shareData.shareType===1)){
					uni.showModal({
						content:"分享内容不能为空",
						showCancel:false
					})
					return;
				}
				if(!shareData.image&&(shareData.shareType===0||shareData.shareType===2)){
					uni.showModal({
						content:"分享内容不能为空",
						showCancel:false
					})
					return;
				}
				let obj={
					provider: e.id, // 服务商
					scene: e.type && e.type === 'WXSenceTimeline' ? 'WXSenceTimeline' : 'WXSceneSession', // 场景 微信好友WXSceneSession  朋友圈WXSceneTimeLine
					type: shareData.shareType, // 图文0 文字1 图片2
					href: shareData.href, // 分享h5地址
					title: "糗事百科分享",
					summary: shareData.shareText, // 描述
					imageUrl: shareData.image,
				}
				// #ifdef APP-PLUS
				await uni.share(obj)
				// #endif
				this.shareData.shareText="你喜欢的都在这里,快来看看吧!"
			}
		},
		created() {
			console.log("aaa")
			//获取设备分享支持
			uni.getProvider({
				service:"share",
				success: (res) => {
					console.log(res)
					let data=[]
					res.provider.forEach(item=>{
						switch(item){
							case "weixin":
								data.push({
									name: "微信好友",
									id:"weixin",
									type: 'WXSceneSession',
									zicon:"icon-weixin",
									sort: 0
								});
								data.push({
									name: "朋友圈",
									id:"weixin",
									type: 'WXSenceTimeline',
									zicon:"icon-weixin",
									sort: 1
								});
								break;
							case "sinaweibo":
								data.push({
									name: "新浪微博",
									id:"sinaweibo",
									type:"WXSenceTimeline",
									zicon:"icon-xinlangweibo",
									sort: 2
								});
								break;
							case "qq":
								data.push({
									name: "QQ好友",
									id:"qq",
									type:'qq',
									zicon:"icon-QQ",
									sort: 3
								});
								break;
							default:
								data.push({
									name: "其它",
									id:"other",
									zicon:"icon-gengduo",
									sort: 1
								});
								break;
						}
					})
					this.provider=data
				}
			})
		}
	}
</script>

<style lang="less" scoped>
	.share_zhezhao{
		position: fixed;
		left: 0;
		bottom: 0;
		right: 0;
		top: 0;
		background-color: hsla(0,0%,0%,.2);
		z-index: 997;
	}
	.share_wrapper{
		box-sizing: border-box;
		position: fixed;
		left: 0;
		bottom: 0;
		width: 100%;
		z-index: 999;
		background-color: #fff;
		box-shadow: 0 -4rpx 5rpx 0 hsla(0,0%,0%,.1);
		.share_title{
			box-sizing: border-box;
			width: 100%;
			text-align: center;
			padding: 20rpx 0;
		}
		.share_list{
			white-space: nowrap;
			height: 180rpx;
			padding: 10rpx 0 30rpx 0;
			border-bottom: 1rpx solid #eee;
			.share_item{
				display: inline-block;
				width: 120rpx;
				text-align: center;
				margin: 0 45rpx;
				.share_img{
					width: 100%;
					font-size: 70rpx;
					line-height: 120rpx;
					color: #fff;
					border-radius: 50%;
					margin-bottom: 10rpx;
				}
				.icon-weixin{
					background-color: #2ad19b;
				}
				.icon-faxian{
					background-color: #514d4c;
				}
				.icon-xinlangweibo{
					background-color: #ee5e5e;
				}
				.icon-QQ{
					background-color: #5280ce;
				}
				.icon-gengduo{
					background-color: #7a7a7a;
				}
				.share_desc{
					font-size: 30rpx;
					color: #888;
				}
			}
		}
		.share_cancel{
			font-size: 35rpx;
			text-align: center;
			line-height: 100rpx;
		}
	}
	.active{
		background-color: #eee;
	}
</style>
