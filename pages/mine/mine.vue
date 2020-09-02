<template>
	<view class="wrapper">
		<!-- 已登录 -->
		<login v-if="isLogin" :mineinfo="mineinfo"/>
		<!-- 未登录 -->
		<view class="nologin_wapper" v-else>
			<view class="nologin_text">登录糗事百科,体验更多功能</view>
			<no-login/>
			<view class="nologin_tologin" @click="jumpToLogin">账号密码登录 <view>></view></view>
		</view>
		<!-- 列表 -->
		<my-tab-list :minedata="minedata"/>
		<!-- 广告 -->
		<image class="ad" :src="ad.url" mode="aspectFill"></image>
		<!-- 选项 -->
		<xuan-xiang-list :list="list" :isLogin="isLogin"/>
	</view>
</template>

<script>
	import noLogin from '../../components/mine/noLogin.vue'
	import login from '../../components/mine/login.vue'
	import myTabList from '../../components/mine/myTabList.vue'
	import xuanXiangList from '../../components/mine/xuanXiangList.vue'
	
	export default {
		data() {
			return {
				isLogin: false,//是否登录
				mineinfo:{
					userpic:"../../static/demo/11.jpg",
					username:"楚绵",
					totalnum:0,
					todaynum:0
				},//用户登录信息
				minedata:[
					{name:"糗事",num:0},
					{name:"动态",num:0},
					{name:"评论",num:0},
					{name:"收藏",num:0}
				],//tab列表项
				list:[
					{icon:"icon-liulan",name:"浏览历史",jumpType:"",path:""},
					{icon:"icon-huiyuanvip",name:"糗百认证",jumpType:"",path:""},
					{icon:"icon-guanyuwomen",name:"审核糗事",jumpType:"",path:""}
				],//功能选项列表
				ad:{
					url:"../../static/demo/demo20.jpg"
				},//广告信息
			};
		},
		components:{
			noLogin,
			login,
			myTabList,
			xuanXiangList
		},
		methods:{
			//跳转到登录页面
			jumpToLogin(){
				uni.navigateTo({
					url: '/pages/login/login'
				});
			},
		},
		onLoad() {
	
		},
		onNavigationBarButtonTap(res) {
			if(res.index===0){
				uni.navigateTo({
					url: '/pages/userSet/userSet'
				});
			}
		}
	}
</script>

<style lang="less" scoped>
	.wrapper{
		box-sizing: border-box;
		padding: 20rpx;
		.nologin_wapper{
			font-size: 32rpx;
			.nologin_text{
				text-align: center;
			}
			.nologin_tologin{
				position: relative;
				display: inline-block;
				left: 50%;
				transform: translateX(-50%);
				margin-bottom:40rpx;
				text-align: center;
				font-size: 30rpx;
				color: #343434;
				view{
					color: #dcdcdc;
					display: inline-block;
				}
			}
		}
		.ad{
			width: 100%;
			height: 180rpx;
			border-radius: 20rpx;
			margin-bottom: 30rpx;
		}
		
	}
	
</style>
