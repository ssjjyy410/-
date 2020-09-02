<template>
	<view class="paper_wrapper" >
		<!-- 信息列表 -->
		<template v-if="paperInfo.list.length>0">
			<scroll-view class="scrollview" :style="{'height':swiperHeight+'px'}" scroll-y>
				<paper-list v-for="(item,index) in paperInfo.list" :paperInfo="item" :key="index"/>
				<load-more :loadContext="paperInfo.loadContext"/>
			</scroll-view>
		</template>
		<template v-else>
			<nothing />
		</template>
		<caidan-card 
			:isShowCaidan="isShowCaidan"
			@addFriends="addFriends"
			@clearAll="clearAll"
			@hideCaidan="hideCaidan"
		/>
	</view>
</template>

<script>
	import uniBadge from '../../components/uni-badge/uni-badge.vue'
	import paperList from '../../components/paper/paperList.vue'
	import loadMore from '../../components/common/loadMore.vue'
	import nothing from '../../components/common/nothing.vue'
	import caidanCard from '../../components/paper/caidanCard.vue'
	
	export default {
		data() {
			return {
				count: 0,
				paperInfo:{
					loadContext: "上拉加载更多",
					list:[
						{
							userpic: "../../static/demo/11.jpg",
							username: "飞屋睿",
							time: "13:58",
							desc: "六道飞鱼家常菜,好吃又下饭,活动优惠更便宜,快快购买!",
							noreadnum: 12
						},
						{
							userpic: "../../static/demo/11.jpg",
							username: "飞屋睿",
							time: "13:58",
							desc: "六道飞鱼家常菜,好吃又下饭,活动优惠更便宜,快快购买!",
							noreadnum: 12
						},
						{
							userpic: "../../static/demo/11.jpg",
							username: "飞屋睿",
							time: "13:58",
							desc: "六道飞鱼家常菜,好吃又下饭,活动优惠更便宜,快快购买!",
							noreadnum: 12
						},
						{
							userpic: "../../static/demo/11.jpg",
							username: "飞屋睿",
							time: "13:58",
							desc: "六道飞鱼家常菜,好吃又下饭,活动优惠更便宜,快快购买!",
							noreadnum: 12
						},
						{
							userpic: "../../static/demo/11.jpg",
							username: "飞屋睿",
							time: "13:58",
							desc: "六道飞鱼家常菜,好吃又下饭,活动优惠更便宜,快快购买!",
							noreadnum: 12
						}
					]
				},
				isShowCaidan: false, //是否显示菜单选项
			};
		},
		components:{
			uniBadge,
			paperList,
			loadMore,
			nothing,
			caidanCard
		},
		onReachBottom(){
			this.loadMore()
		},
		methods:{
			//上拉加载更多
			loadMore(){
				let context=this.paperInfo.loadContext
				if(context!=='上拉加载更多') return;//防止频繁发起服务器请求
				this.paperInfo.loadContext="加载中..."
				setTimeout(()=>{
					this.count+=1
					const shuju=[
						{
							userpic: "../../static/demo/11.jpg",
							username: "飞屋睿",
							time: "13:58",
							desc: "六道飞鱼家常菜,好吃又下饭,活动优惠更便宜,快快购买!",
							noreadnum: 12
						},
						{
							userpic: "../../static/demo/11.jpg",
							username: "飞屋睿",
							time: "13:58",
							desc: "六道飞鱼家常菜,好吃又下饭,活动优惠更便宜,快快购买!",
							noreadnum: 12
						}
					]
					this.paperInfo.list=[...this.paperInfo.list,...shuju]
					this.paperInfo.loadContext="上拉加载更多"
					if(this.count===2){
						this.paperInfo.loadContext="没有更多了"
						this.count=0
					}
				},2000)
			},
			// 菜单
			//加糗友
			addFriends(){
				console.log("加糗友")
				this.hideCaidan()
			},
			//清除所有信息
			clearAll(){
				console.log("清除所有信息")
				this.hideCaidan()
			},
			//显示或隐藏菜单
			showCaidan(){
				this.isShowCaidan=true
			},
			hideCaidan(){
				this.isShowCaidan=false
			}
		},
		onNavigationBarButtonTap(res) {
			let that=this;
			let index=res.index
			switch(index){
				case 0:
					uni.navigateTo({
						url:"/pages/userList/userList"
					})
					break;
				case 1:
					that.isShowCaidan=!that.isShowCaidan;
					break;
			}
		},
		onHide(){
			this.hideCaidan()
		}
	}
</script>

<style lang="less" scoped>
	.active{
		background-color: #eee;
	}
</style>
