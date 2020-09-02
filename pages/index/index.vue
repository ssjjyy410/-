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
						<list-item v-for="(item,index1) in items.list" :key="index1" :item="item" :index1="index1" :index="index" @closeItem="closeItem"/>
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
	import listItem from '../../components/index/listItem.vue'
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
						list:[{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"video",// img:图文,video:视频
							titlepic:"/static/demo/11.jpg",
							video:{
								looknum:'20w',
								long: '2:07'
							},
							infonum:{
								index:0,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						},{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"img",// img:图文,video:视频
							titlepic:"/static/demo/11.jpg",
							infonum:{
								index:1,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						},{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"img",// img:图文,video:视频
							titlepic:"/static/demo/11.jpg",
							infonum:{
								index:2,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						}]
					},
					{
						loadContext:"上拉加载更多",
						list:[{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"video",// img:图文,video:视频
							video:{
								looknum:'20w',
								long: '2:07'
							},
							titlepic:"/static/demo/11.jpg",
							infonum:{
								index:0,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						},{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"img",// img:图文,video:视频
							titlepic:"/static/demo/11.jpg",
							infonum:{
								index:1,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						},{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"img",// img:图文,video:视频
							titlepic:"/static/demo/11.jpg",
							infonum:{
								index:2,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						}]
					},
					{
						loadContext:"上拉加载更多",
						list:[{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"video",// img:图文,video:视频
							video:{
								looknum:'20w',
								long: '2:07'
							},
							titlepic:"/static/demo/11.jpg",
							infonum:{
								index:0,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						},{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"img",// img:图文,video:视频
							titlepic:"/static/demo/touxaing.jpg",
							infonum:{
								index:1,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						},{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"img",// img:图文,video:视频
							titlepic:"/static/demo/11.jpg",
							infonum:{
								index:2,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						}]
					},
					{
						loadContext:"上拉加载更多",
						list:[{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"video",// img:图文,video:视频
							video:{
								looknum:'20w',
								long: '2:07'
							},
							titlepic:"/static/demo/11.jpg",
							infonum:{
								index:0,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						},{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"img",// img:图文,video:视频
							titlepic:"/static/demo/11.jpg",
							infonum:{
								index:1,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						},{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"img",// img:图文,video:视频
							titlepic:"/static/demo/touxaing.jpg",
							infonum:{
								index:2,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						}]
					},
					{
						loadContext:"上拉加载更多",
						list:[{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"video",// img:图文,video:视频
							video:{
								looknum:'20w',
								long: '2:07'
							},
							titlepic:"/static/demo/11.jpg",
							infonum:{
								index:0,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						},{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"img",// img:图文,video:视频
							titlepic:"/static/demo/11.jpg",
							infonum:{
								index:1,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						},{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"img",// img:图文,video:视频
							titlepic:"/static/demo/touxaing.jpg",
							infonum:{
								index:2,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						}]
					},
					{
						loadContext:"上拉加载更多",
						list:[{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"video",// img:图文,video:视频
							video:{
								looknum:'20w',
								long: '2:07'
							},
							titlepic:"/static/demo/11.jpg",
							infonum:{
								index:0,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						},{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"img",// img:图文,video:视频
							titlepic:"/static/demo/touxaing.jpg",
							infonum:{
								index:1,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						},{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"img",// img:图文,video:视频
							titlepic:"/static/demo/touxaing.jpg",
							infonum:{
								index:2,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
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
			"list-item":listItem,
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
				console.log(index)
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
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"video",// img:图文,video:视频
							video:{
								looknum:'20w',
								long: '2:07'
							},
							titlepic:"/static/demo/touxaing.jpg",
							infonum:{
								index:0,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						},{
							userpic:"/static/demo/touxaing.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"我是标题",
							type:"video",// img:图文,video:视频
							video:{
								looknum:'20w',
								long: '2:07'
							},
							titlepic:"/static/demo/touxaing.jpg",
							infonum:{
								index:0,//0:没有操作，1：顶，2：踩
								dingnum:11,
								cainum:11
							},
							commentnum:20,
							sharenum:10
						},
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
			}
			
		}
	}
</style>
