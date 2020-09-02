<template>
	<view>
		<!-- 详情 -->
		<detail-info :item="list"/>
		<!-- 评论 -->
		<view class="comment_wrapper">
			<view class="comment_header">最新评论 {{comment.count>0?comment.count:''}}</view>
			<template v-if="comment.count>0">
				<scroll-view scroll-y>
					<template v-for="(item,index) in comment.list">
						<comment-wrapper :list="item" :key="index"/>
					</template>
					<load-more :loadContext="comment.loadContext"/>
				</scroll-view>
			</template>
			<template v-else>
				<nothing />
			</template>
		</view>
		<!-- 输入框 -->
		<chat-input @tapFabu="tapFabu"/>
		<!-- 分享 -->
		<share-card 
			:isShowFenxiang="isShowFenxiang" 
			@hideFenxiang="hideFenxiang"
			:list="list"
		/>
	</view>
</template>

<script>
	import detailInfo from '../../components/detail/detailInfo.vue'
	import commentWrapper from '../../components/detail/commentWrapper.vue'
	import loadMore from '../../components/common/loadMore.vue'
	import nothing from '../../components/common/nothing.vue'
	import chatInput from '../../components/paper/chatInput.vue'
	import shareCard from '../../components/detail/shareCard.vue'
	import time from '../../common/time.js'
	
	export default {
		data() {
			return {
				count: 0,
				itemDetail:{},//用户信息
				list:{//图文
					userpic: "../../static/demo/touxaing.jpg",
					username: "猪猪",
					sex: 1,//0 男，1 女
					age: 18,
					isGuanzhu: true,
					title: "开心呀",
					titlepic: "../../static/demo/touxaing.jpg",
					morepic:[
						"../../static/demo/touxaing.jpg",
						"../../static/demo/2.jpg",
						"../../static/demo/3.jpg",
						"../../static/demo/4.jpg",
						"../../static/demo/5.jpg"
					],
					video:false,
					share: false,
					path: '成都 金华',
					sharenum: 22,
					commentnum: 31,
					goodnum: 10
				},
				comment:{
					count: 9,//评论数
					loadContext: "上拉加载更多",
					list:[]
				},
				//模拟后端评论数据
				houduanCommentList:[
					{
						id:"2",//用户ID
						fid:0,//一级评论
						username:"猪猪",
						userpic: "../../static/demo/11.jpg",
						time:"1598852796",//评论时间
						replytoUser:{
							id:"1",
							username:"费武瑞"
						},
						data:"真惨啊",
						reply:[
							{
								id:"1",
								fid:1,//二级评论
								username:"费武瑞",
								userpic: "../../static/demo/touxaing.jpg",
								time:"1598852852",//评论时间
								replytoUser:{
									id:"2",
									username:"猪猪"
								},
								data:"你懂个屁"
							},
							{
								id:"2",
								fid:1,
								username:"猪猪",
								userpic: "../../static/demo/11.jpg",
								time:"1598852852",
								replytoUser:{
									id:"1",
									username:"费武瑞"
								},
								data:"NM$L"
							}
						]
					},
					{
						id:"3",
						fid:0,//一级评论
						username:"大神",
						userpic: "../../static/demo/2.jpg",
						time:"1598680052",//评论时间
						replytoUser:{
							id:"1",
							username:"费武瑞"
						},
						data:"你这不算什么",
						reply:[
							{
								id:"1",
								fid:1,//二级评论
								username:"费武瑞",
								userpic: "../../static/demo/touxaing.jpg",
								time:"1598680545",//评论时间
								replytoUser:{
									id:"3",
									username:"大神"
								},
								data:"你试试"
							},
							{
								id:"3",
								fid:1,
								username:"大神",
								userpic: "../../static/demo/2.jpg",
								time:"1598716545",
								replytoUser:{
									id:"1",
									username:"费武瑞"
								},
								data:"牛逼"
							}
						]
					},
					{
						id:"2",//用户ID
						fid:0,//一级评论
						username:"猪猪",
						userpic: "../../static/demo/11.jpg",
						time:"1598852796",//评论时间
						replytoUser:{
							id:"1",
							username:"费武瑞"
						},
						data:"真惨啊",
						reply:[
							{
								id:"1",
								fid:1,//二级评论
								username:"费武瑞",
								userpic: "../../static/demo/touxaing.jpg",
								time:"1598852852",//评论时间
								replytoUser:{
									id:"2",
									username:"猪猪"
								},
								data:"你懂个屁"
							},
							{
								id:"2",
								fid:1,
								username:"猪猪",
								userpic: "../../static/demo/11.jpg",
								time:"1598852852",
								replytoUser:{
									id:"1",
									username:"费武瑞"
								},
								data:"NM$L"
							}
						]
					},
				],
				isShowFenxiang:false,//是否显示分享面板
			}
		},
		methods: {
			// 上拉加载更多
			loadMore(){
				let context=this.comment.loadContext
				if(context!=='上拉加载更多') return;//防止频繁发起服务器请求
				let houduanCommentList=this.houduanCommentList
				this.comment.loadContext="加载中..."
				setTimeout(()=>{
					// 模拟后端获取数据
					let arr=houduanCommentList.slice(this.count,(houduanCommentList.length<this.count+2)?houduanCommentList.length:this.count+2)
					this.comment.list=[...this.comment.list,...arr]
					this.count+=2;
					this.comment.loadContext="上拉加载更多"
					if(houduanCommentList.length===this.comment.list.length){
						this.comment.loadContext="没有更多了"
					}
				},2000)
			},
			//发送消息
			tapFabu(text){
				if(text==='') return;
				//将text发送到后端
				setTimeout(()=>{
					//这里模拟后端的数据
					const shuju=[
						{
							id:"222",//用户ID
							fid:0,//一级评论
							username:"Sam",
							userpic: "../../static/demo/4.jpg",
							time:new Date().getTime(),//评论时间
							replytoUser:{
								id:"1",
								username:"费武瑞"
							},
							data: text,
							reply:[
								{
									id:"1",
									fid:1,//二级评论
									username:"费武瑞",
									userpic: "../../static/demo/touxaing.jpg",
									time:"1598857428",//评论时间
									replytoUser:{
										id:"222",
										username:"Sam"
									},
									data:"都滚吧"
								}
							]
						},
					]
					this.comment.list=[...this.houduanCommentList,...shuju]
				},2000)
			},
			//隐藏分享面板
			hideFenxiang(){
				this.isShowFenxiang=false
			},
			//显示分享面板
			showFenxiang(){
				this.isShowFenxiang=true
			},
		},
		components:{
			detailInfo,
			commentWrapper,
			loadMore,
			nothing,
			chatInput,
			shareCard
		},
		onLoad(options) {
			//获取页面间传递的用户信息
			this.itemDetail=JSON.parse(options.itemDetail)
			// 进入页面：模拟后端获取数据
			setTimeout(()=>{
				let arr=this.houduanCommentList.slice(this.count,2)
				this.comment.list=[...this.comment.list,...arr]
				this.count+=2
			},2000)
			
		},
		onReady() {
			//设置标题
			uni.setNavigationBarTitle({
			    title: this.itemDetail.username
			});
		},
		onNavigationBarButtonTap(res) {
			if(res.index===0){
				this.isShowFenxiang=!this.isShowFenxiang
			}
		},
		onReachBottom() {
			this.loadMore()
		}
	}
</script>

<style lang="less" scoped>
	.comment_wrapper{
		box-sizing: border-box;
		padding: 20rpx;
		border-top: 1rpx solid #f2f2f2;
		.comment_header{
			font-weight: bold;
			
		}
		scroll-view{
			
		}
	}
	
</style>
