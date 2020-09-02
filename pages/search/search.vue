<template>
	<view >
		<template v-if="isNoList">
			<scroll-view :style="{height:swiperHeight+'px'}" scroll-y @scrolltolower="loadMore()">
				<list-item v-for="(item,index) in newslist.list" :key="index" :item="item" :index="index" @closeItem="closeItem"/>
				<load-more v-if="newslist.list.length>0" :loadContext="newslist.loadContext"/>
			</scroll-view>
		</template>
		<template v-else>
			<nothing />
		</template>
	</view>
</template>

<script>
	import listItem from '../../components/index/listItem.vue'
	import loadMore from '../../components/common/loadMore.vue'
	import nothing from '../../components/common/nothing.vue'
	
	export default {
		data() {
			return {
				count: 0,
				text: "",//关键字
				isSearched: false,//是否搜索过，用于决定第一次搜索前不显示为空图片和为空时显示为空图片
				newslist:{
					loadContext:"上拉加载更多",
					list:[]
				},
			};
		},
		components:{
			listItem,
			loadMore,
			nothing
		},
		computed:{
			isNoList(){
				return !this.isSearched||this.newslist.list.length>0
			}
		},
		methods:{
			//关闭该项
			closeItem(i){
				let index=i.index;
				this.newslist.list.splice(index,1)
			},
			//上拉加载更多
			loadMore(index){
				let context=this.newslist.loadContext
				if(context!=='上拉加载更多') return;//防止频繁发起服务器请求
				this.newslist.loadContext="加载中..."
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
					this.newslist.list=[...this.newslist.list,...shuju]
					this.newslist.loadContext="上拉加载更多"
					if(this.count===2){
						this.newslist.loadContext="没有更多了"
						this.count=0
					}
				},2000)
			},
			//搜索,获取数据
			getData(text){
				this.text=text;
				//输入为空，返回
				if(this.text==='') return;
				if(this.timeoutId) clearTimeout(this.timeoutId);//取消上一次的请求
				uni.showLoading()
				this.timeoutId=setTimeout(()=>{
					//发送请求
					this.isSearched=true//搜索过，是否显示为空图片由搜索结果而定
					if(this.text==='dd') this.newslist.list=[
						{
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
						},
						{
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
						},
						{
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
						},
					]
					else{
						this.newslist.list=[]
					}
					uni.hideLoading()
				},3000)
			}
		},
		//点击取消
		onNavigationBarButtonTap(res){
			if(res.index===0){
				uni.navigateBack({
					delta:1
				})
			}
		},
		//搜索确认
		onNavigationBarSearchInputConfirmed(res){
			this.getData(res.text)
			// 手机端收起键盘
			// #ifdef APP-PLUS
			plus.key.hideSoftKeybord();
			// #endif
		}
	}
</script>

<style lang="less" scoped>

</style>
