<template>
	<view class="index_wrapper">
		<tab-bar @tabTap="tabTap" :tabBars="tabBars" :tabIndex="tabIndex"/>
		<swiper 
			class="swiper u_list" 
			:current="current"
			:style="{height:swiperHeight+'px'}"
			@change="swiperChange"
		>
			<swiper-item v-for="(items,index) in newsList" :key="index">
				<template v-if="items.list.length>0">
					<scroll-view scroll-y @scrolltolower="loadMore(index)">
						<topic-list v-for="(item,index1) in items.list" :list="item" :key="index1"/>
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
	import topicList from '../../components/dynamic/topicList.vue'
	import tabBar from '../../components/index/tabBar.vue'
	import loadMore from '../../components/common/loadMore.vue'
	import nothing from '../../components/common/nothing.vue'
	
	export default {
		data() {
			return {
				count:0,
				tabIndex:1,
				current:1,
				newsList:[
					{
						loadContext:"上拉加载更多",
						list:[
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
							}]
					},
					{
						loadContext:"上拉加载更多",
						list:[
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
							}]
					},
					{
						loadContext:"上拉加载更多",
						list:[
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
							}]
					},
					{
						loadContext:"上拉加载更多",
						list:[
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
							}]
					},
					{
						loadContext:"上拉加载更多",
						list:[
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
							}]
					},
					{
						loadContext:"上拉加载更多",
						list:[
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
							}]
					}
				],
				tabBars:[
					{name:"关注",id:"guanzhu"},
					{name:"推荐",id:"tuijian"},
					{name:"体育",id:"tiyu"},
					{name:"热点",id:"redian"},
					{name:"财经",id:"caijing"},
					{name:"娱乐",id:"yule"}
				]
			}
		},
		components:{
			topicList,
			"tab-bar": tabBar,
			"load-more": loadMore,
			"nothing": nothing
		},
		onNavigationBarButtonTap(res) {
			switch(res.index){
				case 0:
					console.log("签到");
					break;
				case 1:
					uni.navigateTo({
						url:"/pages/publish/publish"
					})
					break;
			}
		},
		onNavigationBarSearchInputClicked(){
			uni.navigateTo({
				url:"/pages/search/search"
			})
		},
		methods: {
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
				let context=this.newsList[index].loadContext
				if(context!=='上拉加载更多') return;//防止频繁发起服务器请求
				this.newsList[index].loadContext="加载中..."
				setTimeout(()=>{
					this.count+=1
					const shuju=[
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
					this.newsList[index].list=[...this.newsList[index].list,...shuju]
					this.newsList[index].loadContext="上拉加载更多"
					if(this.count===2){
						this.newsList[index].loadContext="没有更多了"
						this.count=0
					}
				},2000)
			},
			//关闭某选项
			closeItem({index,index1}){
				this.newsList[index].list.splice(index1,1)
			}
		}
	}
</script>

<style lang="less" scoped>
	.index_wrapper{
		.u_list{
			scroll-view{
				height: 100%;
				min-height: 100%;
				padding: 0 20rpx;
			}
			
		}
	}
</style>
