<template>
	<view>
		<news-nav 
			:left="'icon-qiandao'" 
			:right="'icon-fabu'" 
			:navBars="navBars" 
			@toggleNav="toggleNav" 
			@handleRightClick="tapFabu" 
			@handleLeftClick="tapQiandao" 
			:navIndex="navIndex"
		/>
		<view :style="{'width':'100%','height':customBar+'px'}">
		    <!-- 这里是状态栏 -->
		</view>
		<!-- 公共组件 -->
		<swiper
			class="swiper list_wrapper" 
			:current="current"
			:style="{height:swiperHeight+'px'}"
			@change="swiperChange"
		>
			<!-- 关注 -->
			<swiper-item>
				<template v-if="guanzhu.list.length>0">
					<scroll-view scroll-y @scrolltolower="loadMore()">
						<common-list v-for="(item,index) in guanzhu.list" :item="item" :index="index" @closeItem="closeItem" :key="index"/>
						<load-more :loadContext="guanzhu.loadContext"/>
					</scroll-view>
				</template>
				<template v-else>
					<nothing />
				</template>
			</swiper-item>
			<!-- 话题 -->
			<swiper-item>
				<scroll-view scroll-y>
					<!-- 搜索框 -->
					<view class="search">
						<input class="input" type="text" v-model="text" placeholder="搜索内容" placeholder-class="icon iconfont icon-sousuo input-placeholder"/>
					</view>
					<!-- 轮播图 -->
					<swiper class="swiper_wrapper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1500">
						<swiper-item v-for="(item,index) in banners" :key="index">
							<image :src="item.url" mode="aspectFill"></image>
						</swiper-item>
					</swiper>
					<!-- 热门分类 -->
					<hot-nav :hotNavs="hotNavs" @jumpTo="jumpToTopic"/>
					<!-- 最近更新 -->
					<view class="zuijin_wrapper">
						<view class="zuijin_header">最近更新</view>
						<topic-list v-for="(item,index) in topic" :key="index" :list="item"/>
					</view>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	import newsNav from '../../components/dynamic/newsNav.vue'
	import commonList from '../../components/common/commonList.vue'
	import loadMore from '../../components/common/loadMore.vue'
	import nothing from '../../components/common/nothing.vue'
	import hotNav from '../../components/dynamic/hotNav.vue'
	import topicList from '../../components/dynamic/topicList.vue'
	
	export default {
		data() {
			return {
				count: 0,
				navIndex:0,//导航栏下标
				current: 0,
				navBars:[
					{name:"关注",id:"guanzhu"},
					{name:"话题",id:"huati"}
				],//导航栏
				guanzhu:{
					loadContext: "上拉加载更多",
					list: [
						//文字
						{
							userpic: "../../static/demo/touxaing.jpg",
							username: "三余先生",
							sex: 0,//0 男，1 女
							age: 25,
							isGuanzhu: false,
							title: "我是标题",
							titlepic: "",
							video: false,
							share: false,
							path: '深圳 龙岗',
							sharenum: 20,
							commentnum: 30,
							goodnum: 20
							
						},
						//图文
						{
							userpic: "../../static/demo/touxaing.jpg",
							username: "猪猪",
							sex: 1,//0 男，1 女
							age: 18,
							isGuanzhu: true,
							title: "开心呀",
							titlepic: "../../static/demo/touxaing.jpg",
							video: false,
							share: false,
							path: '成都 金华',
							sharenum: 22,
							commentnum: 31,
							goodnum: 10
							
						},
						//视频
						{
							userpic: "../../static/demo/touxaing.jpg",
							username: "张三",
							sex: 1,//0 男，1 女
							age: 18,
							isGuanzhu: false,
							title: "水经验啦",
							titlepic: "../../static/demo/11.jpg",
							video: {
								looknum: "22w",
								long: "2:47"
							},
							share: false,
							path: '成都 金华',
							sharenum: 22,
							commentnum: 31,
							goodnum: 10
							
						},
						//分享
						{
							userpic: "../../static/demo/touxaing.jpg",
							username: "李四",
							sex: 0,//0 男，1 女
							age: 30,
							isGuanzhu: true,
							title: "分享一个东西",
							titlepic: "",
							video: false,
							share: {
								title: "男人的秘密",
								titlepic: "../../static/demo/11.jpg"
							},
							path: '成都 金华',
							sharenum: 22,
							commentnum: 31,
							goodnum: 10
							
						}
					]
				},//关注
				text: '',//搜索关键字
				banners:[
					{"url":'../../static/demo/banner1.jpg'},
					{"url":'../../static/demo/banner2.jpg'},
					{"url":'../../static/demo/banner3.jpg'}
				],//轮播图
				hotNavs:[
					{"name":'最新'},
					{"name":'游戏'},
					{"name":'情感'},
					{"name":'打卡'},
					{"name":'故事'},
					{"name":'喜爱'}
				],//热门分类
				topic:[
					{
						title: '#淘宝记录#',
						titlepic: '../../static/demo/11.jpg',
						dec: '120斤到85斤 我得反转人生',
						totalnum: 545,
						todaynum: 720
					},
					{
						title: '#淘宝记录#',
						titlepic: '../../static/demo/11.jpg',
						dec: '120斤到85斤 我得反转人生',
						totalnum: 545,
						todaynum: 720
					},
					{
						title: '#淘宝记录#',
						titlepic: '../../static/demo/11.jpg',
						dec: '120斤到85斤 我得反转人生',
						totalnum: 545,
						todaynum: 720
					},
					{
						title: '#淘宝记录#',
						titlepic: '../../static/demo/11.jpg',
						dec: '120斤到85斤 我得反转人生',
						totalnum: 545,
						todaynum: 720
					},
					{
						title: '#淘宝记录#',
						titlepic: '../../static/demo/11.jpg',
						dec: '120斤到85斤 我得反转人生',
						totalnum: 545,
						todaynum: 720
					},
					{
						title: '#淘宝记录#',
						titlepic: '../../static/demo/11.jpg',
						dec: '120斤到85斤 我得反转人生',
						totalnum: 545,
						todaynum: 720
					},
					{
						title: '#淘宝记录#',
						titlepic: '../../static/demo/11.jpg',
						dec: '120斤到85斤 我得反转人生',
						totalnum: 545,
						todaynum: 720
					}
				]
			};
		},
		components:{
			newsNav,
			commonList,
			loadMore,
			nothing,
			hotNav,
			topicList
		},
		methods:{
			//导航栏切换
			toggleNav(index){
				this.navIndex=index
				this.current=index
			},
			//跳转到发布页面
			tapFabu(){
				uni.navigateTo({
					url:"/pages/publish/publish"
				})
			},
			//跳转到签到页面
			tapQiandao(){
				console.log("签到")
			},
			//滑动事件
			swiperChange(event){
				this.navIndex=event.detail.current
			},
			//上拉加载更多
			loadMore(){
				let context=this.guanzhu.loadContext
				if(context!=='上拉加载更多') return;//防止频繁发起服务器请求
				this.guanzhu.loadContext="加载中..."
				setTimeout(()=>{
					this.count+=1
					const shuju=[
						//图文
						{
							userpic: "../../static/demo/touxaing.jpg",
							username: "猪猪",
							sex: 1,//0 男，1 女
							age: 18,
							isGuanzhu: true,
							title: "开心呀",
							titlepic: "../../static/demo/touxaing.jpg",
							video: false,
							share: false,
							path: '成都 金华',
							sharenum: 22,
							commentnum: 31,
							goodnum: 10
							
						},
						//视频
						{
							userpic: "../../static/demo/touxaing.jpg",
							username: "张三",
							sex: 1,//0 男，1 女
							age: 18,
							isGuanzhu: false,
							title: "水经验啦",
							titlepic: "../../static/demo/11.jpg",
							video: {
								looknum: "22w",
								long: "2:47"
							},
							share: false,
							path: '成都 金华',
							sharenum: 22,
							commentnum: 31,
							goodnum: 10
							
						}
					]
					this.guanzhu.list=[...this.guanzhu.list,...shuju]
					this.guanzhu.loadContext="上拉加载更多"
					if(this.count===2){
						this.guanzhu.loadContext="没有更多了"
						this.count=0
					}
				},2000)
			},
			//删除某选项
			closeItem(index){
				this.guanzhu.list.splice(index,1)
			},
			//跳转到话题分类页面
			jumpToTopic(){
				uni.navigateTo({
					url:"/pages/topic/topic"
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.list_wrapper{
		width: 100%;
		scroll-view{
			height: 100%;
			.search{
				width: 100%;
				.input{
					margin: 20rpx;
					padding: 20rpx;
					border-radius: 15rpx;
					background-color: #f4f4f4;
				}
				.input-placeholder{
					color: #a1a1a1;
					text-align: center;
				}
			}
			.swiper_wrapper{
				box-sizing: border-box;
				width: 100%;
				padding: 0 20rpx 20rpx;
				border-radius: 15rpx;
				border-bottom: 1px solid #eee;
				
				swiper-item{
					width: 100%;
					border-radius: 15rpx;
					image{
						width: 100%;
						transform: translateY(-17%);
					}
				}
			}
			.zuijin_wrapper{
				margin: 20rpx;
				.zuijin_header{
					width: 100%;
					font-size: 35rpx;
				}
				margin-bottom: var(--window-bottom);
			}
			
		}
	}
	
</style>
