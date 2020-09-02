<template>
	<view class="detail_wrapper">
		<topic-info :topicInfo="topicInfo"/>
		<tab-bar 
			:tabStyle="{width:'50%'}" 
			:tabBars="tabBars" 
			:tabIndex="tabIndex"
			@tabTap="tabTap"
		/>
		<swiper
			class="swiper u_list" 
			:current="current"
			:style="{height:swiperHeight+'px'}"
			@change="swiperChange"
		>
			<swiper-item v-for="(items,index) in newsList" :key="index">
				<template v-if="items.list.length>0">
					<scroll-view scroll-y @scrolltolower="loadMore(index)">
						<common-list v-for="(item,index1) in items.list" :item="item" :index="index1" @closeItem="closeItem" :key="index1"/>
						<load-more :loadContext="items.loadContext"/>
					</scroll-view>
				</template>
				<template v-else>
					<nothing />
				</template>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	import topicInfo from '../../components/common/topicInfo.vue'
	import tabBar from '../../components/index/tabBar.vue'
	import commonList from '../../components/common/commonList.vue'
	import loadMore from '../../components/common/loadMore.vue'
	import nothing from '../../components/common/nothing.vue'
	
	export default {
		data() {
			return {
				count: 0,
				tabIndex: 0,
				current: 0,
				tabBars: [
					{name:"默认",id:"default"},
					{name:"最新",id:"zuixin"}
				],
				topicInfo:{
					"topicpic": "../../static/demo/11.jpg",
					"topictitle": "#忆往事,敬余生#",
					"dynamicnum": 793,
					"todaynum": 641,
					"desc": "面试官：哒哒哒哒哒哒多多多多多多多多多多多多多多多多多多多多多多多多"
				},
				newsList: [
					{
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
					},
					{
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
					},
				]
			};
		},
		components:{
			topicInfo,
			tabBar,
			commonList,
			loadMore,
			nothing
		},
		//下拉刷新事件
		onPullDownRefresh(){
			this.getData()
		},
		onReady() {
			//设置标题
			uni.setNavigationBarTitle({
			    title: this.topicInfo.topictitle
			});
		},
		methods:{
			//导航栏点击事件
			tabTap(index){
				this.tabIndex=index
				this.current=index
			},
			//滑动事件
			swiperChange(event){
				this.tabIndex=event.detail.current
			},
			//上拉加载更多
			loadMore(index){
				//停止下拉刷新事件
				clearTimeout(this.timeoutId)//不要忘了取消异步请求
				uni.stopPullDownRefresh()//这是停止当前页面的下拉刷新，但还是需要手动取消已发送的异步刷新请求
				//加载更多
				let context=this.newsList[index].loadContext
				if(context!=='上拉加载更多') return;//防止频繁发起服务器请求
				this.newsList[index].loadContext="加载中..."
				setTimeout(()=>{
					this.count+=1
					const shuju=[
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
					this.newsList[index].list=[...this.newsList[index].list,...shuju]
					this.newsList[index].loadContext="上拉加载更多"
					if(this.count===2){
						this.newsList[index].loadContext="没有更多了"
						this.count=0
					}
				},2000)
			},
			//获取数据
			getData(){
				this.timeoutId=setTimeout(()=>{
					this.newsList[this.tabIndex].list[0].title="下拉刷新后,标题变了"
					//停止下拉刷新事件
					uni.stopPullDownRefresh()
				},6000)
			},
			//删除某选项
			closeItem(index){
				this.newsList[this.tabIndex].list.splice(index,1)
			}
		}
	}
</script>

<style lang="less" scoped>
	.detail_wrapper{
		.u_list{
			scroll-view{
				height: 100%;
				min-height: 100%;
			}
			
		}
	}
</style>
