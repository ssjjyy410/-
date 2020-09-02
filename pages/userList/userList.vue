<template>
	<view>
		<tab-bar
			:tabStyle="{width:'33%'}" 
			:tabBars="tabBars" 
			:tabIndex="tabIndex"
			@tabTap="tabTap"
		/>
		<!-- 用户列表 -->
		<swiper
			class="userlist_wrapper" 
			:current="current"
			:style="{height:swiperHeight+'px'}"
			@change="swiperChange"
		>
			<swiper-item v-for="(items,index) in userList" :key="index">
				<template v-if="items.list.length>0">
					<scroll-view scroll-y @scrolltolower="loadMore(index)">
						<user-info v-for="(item,index1) in items.list" :key="index1" :index="index1" :item="item" @toggleGuanzhu="toggleGuanzhu"/>
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
	import tabBar from '../../components/index/tabBar.vue'
	import userInfo from '../../components/paper/userInfo.vue'
	import loadMore from '../../components/common/loadMore.vue'
	import nothing from '../../components/common/nothing.vue'
	
	export default {
		data() {
			return {
				count: 0,
				current:0,
				tabIndex:0,
				tabBars: [
					{name:"互关",id:"huguan",num:11},
					{name:"关注",id:"guanzhu",num:10},
					{name:"粉丝",id:"fensi",num:185}
				],
				userList:[
					{
						loadContext: "上拉加载更多",
						list:[
							{
								userpic: "../../static/demo/11.jpg",
								username: "60King",
								sex: 0,
								age: 20,
								isGuanzhu: true
							},
							{
								userpic: "../../static/demo/11.jpg",
								username: "60King",
								sex: 0,
								age: 20,
								isGuanzhu: true
							},
							{
								userpic: "../../static/demo/11.jpg",
								username: "60King",
								sex: 0,
								age: 20,
								isGuanzhu: true
							}
						]
					},
					{
						loadContext: "上拉加载更多",
						list:[
							{
								userpic: "../../static/demo/11.jpg",
								username: "60King",
								sex: 0,
								age: 20,
								isGuanzhu: true
							},
							{
								userpic: "../../static/demo/11.jpg",
								username: "60King",
								sex: 0,
								age: 20,
								isGuanzhu: true
							},
							{
								userpic: "../../static/demo/11.jpg",
								username: "60King",
								sex: 0,
								age: 20,
								isGuanzhu: true
							}
						]
					},
					{
						loadContext: "上拉加载更多",
						list:[
							{
								userpic: "../../static/demo/11.jpg",
								username: "60King",
								sex: 0,
								age: 20,
								isGuanzhu: false
							},
							{
								userpic: "../../static/demo/11.jpg",
								username: "60King",
								sex: 0,
								age: 20,
								isGuanzhu: false
							},
							{
								userpic: "../../static/demo/11.jpg",
								username: "60King",
								sex: 0,
								age: 20,
								isGuanzhu: false
							}
						]
					}
				]
			};
		},
		components:{
			tabBar,
			userInfo,
			loadMore,
			nothing
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
				let context=this.userList[index].loadContext
				if(context!=='上拉加载更多') return;//防止频繁发起服务器请求
				this.userList[index].loadContext="加载中..."
				setTimeout(()=>{
					this.count+=1
					const shuju=[
						{
							userpic: "../../static/demo/11.jpg",
							username: "60King",
							sex: 0,
							age: 20,
							isGuanzhu: true
						},
						{
							userpic: "../../static/demo/11.jpg",
							username: "60King",
							sex: 0,
							age: 20,
							isGuanzhu: true
						},
					]
					this.userList[index].list=[...this.userList[index].list,...shuju]
					this.userList[index].loadContext="上拉加载更多"
					if(this.count===2){
						this.userList[index].loadContext="没有更多了"
						this.count=0
					}
				},2000)
			},
			//是否关注
			toggleGuanzhu(index){
				this.userList[this.tabIndex].list[index].isGuanzhu=true
			}
		},
		onNavigationBarButtonTap(res){
			if(res.index===0){
				uni.navigateBack({
					delta:1
				})
			}
		},
	}
</script>

<style lang="less" scoped>
	.userlist_wrapper{
		scroll-view{
			height: 100%;
			min-height: 100%;
		}
	}
</style>
