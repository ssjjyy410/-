<template>
	<view class="list_item animate__animated animate__fadeInLeft">
		<!-- 头像 -->
		<image class="userpic" :src="item.userpic" mode="aspectFill"></image>
		<view>
			<!-- 页头 -->
			<view class="list_header">
				<view class="header_left">
					<view class="username">{{item.username}}</view>
					<user-sex :sex="item.sex" :age="item.age"/>
				</view>
				<view class="header_right">
					<view class="guanzhu icon iconfont" :class="item.isGuanzhu?'':'icon-zengjia'" @click="toggleGuanzhu">{{item.isGuanzhu?'已关注':'关注'}}</view>
					<!-- <view class="close icon iconfont icon-guanbi" @click="closeItem"></view> -->
				</view> 
			</view>
			<view class="day">26天前</view>
			<!-- 标题 -->
			<view class="title">
				{{item.title}}
			</view>
			<!-- 图片 -->
			<view class="videoOrImg" v-if="item.morepic.length>0">
				<template v-for="(url,index) in item.morepic">
					<image :src="url" mode="widthFix" lazy-load :key="index" @click="previewImg(index)"></image>
				</template>
			</view>
			<!-- 视频 -->
			<view class="videoOrImg" v-if="item.video">
				<image v-if="item.titlepic" :src="item.titlepic" mode="widthFix" lazy-load></image>
				<template>
					<view class="icon iconfont icon-bofang"></view>
					<view class="video_jilu">
						{{item.video.looknum}}<view class="txt">次播放</view>{{item.video.long}}
					</view>
				</template>
			</view>
			<!-- 分享 -->
			<view class="fenxing_xiaoxi" v-if="item.share">
				<image :src="item.share.titlepic" mode="widthFix"></image>
				<view class="fenxing_content">
					{{item.share.title}}
				</view>
			</view>
			<!-- 页尾 -->
			<view class="footer">
				<view class="location">
					{{item.path}}
				</view>
				<view class="func">
					<view class="icon iconfont icon-zhuanfa"></view>
					<view class="fenxiang_num">{{item.sharenum}}</view>
					<view class="icon iconfont icon-pinglun1"></view>
					<view class="fenxiang_num">{{item.commentnum}}</view>
					<template >
						<view class="icon iconfont icon-dianzan" :class="{'active': isDing}" @click="dingTap"></view>
						<view class="fenxiang_num" :class="{'active': isDing}" @click="dingTap">{{item.goodnum}}</view>
					</template>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import userSex from '../common/userSex.vue'
	
	export default {
		data() {
			return {
				isDing: false,//是否点过赞
			};
		},
		components:{
			userSex
		},
		props:["item"],
		methods:{
			// 预览图片
			previewImg(index){
				uni.previewImage({
					urls:this.item.morepic,
					current:index,
					indicator:"number",
					loop:true
				})
			},
			//关注或取消关注
			toggleGuanzhu(){
				this.item.isGuanzhu=!this.item.isGuanzhu
				uni.showToast({
					title:"成功"
				})
			},
			//顶
			dingTap(){
				if(this.isDing){
					this.item.goodnum--;
				}else{
					this.item.goodnum++;
				}
				this.isDing=!this.isDing;
			},
		}
	}
</script>

<style lang="less" scoped>
	@import "../../common/common-list.less";
	
	.day{
		display: block;
		font-size: 28rpx;
		color: #cdcdcd;
		margin-top: 20rpx;
	}
	.list_item{
		.userpic+view{
			border-bottom: none;
		}
	}
</style>
