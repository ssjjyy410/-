<template>
	<view class="wrapper">
		<news-nav 
			:left="'icon-fanhui'" 
			:right="'icon-user_icon'" 
			:navBars="[{'name':username,'id':'username'}]"
			@handleRightClick="seeUserInfo"
			@handleLeftClick="goBack"
		/>
		<chat-input @tapFabu="tapFabu"/>
		<!-- 聊天 -->
		<view class="xiaoxi_list">
			<view :style="{'width':'100%','height':customBar+'px'}">
			    <!-- 这里是状态栏 -->
			</view>
			<template v-for="(xiaoxi,index) in xiaoxis">
				<view class="chat_item_top">
					<xiaoxi-list :xiaoxi="xiaoxi" :index="index" :key="index"/>
				</view>
			</template>
		</view>
	</view>
</template>

<script>
	import newsNav from '../../components/dynamic/newsNav.vue'
	import chatInput from '../../components/paper/chatInput.vue'
	import xiaoxiList from '../../components/paper/xiaoxiList.vue'
	import time from '../../common/time.js'
	
	export default {
		data() {
			return {
				xiaoXiHeight:0,//滚动到底部
				isFirst:true,//是否是第一次进来
				username:'九月',
				xiaoxis:[
					{
						isme:false,
						userpic:"../../static/demo/11.jpg",
						type: "text",
						data: "在吗",
						time: "1567124061",
					},
					{
						isme:false,
						userpic:"../../static/demo/11.jpg",
						type: "text",
						data: "在吗",
						time: "1567167261",
					},
					{
						isme:false,
						userpic:"../../static/demo/11.jpg",
						type: "text",
						data: "在吗",
						time: "1598246988",
					},
					{
						isme:true,
						userpic:"../../static/demo/banner3.jpg",
						type: "text",
						data: "发张照片看看",
						time: "1598281221",
					},
					{
						isme:false,
						userpic:"../../static/demo/11.jpg",
						type: "img",
						data: "../../static/demo/banner3.jpg",
						time: "1598746341",
					},
					{
						isme:true,
						userpic:"../../static/demo/banner3.jpg",
						type: "text",
						data: "啊啊啊啊啊啊啊啊啊",
						time: "1598746461",
					},
					{
						isme:true,
						userpic:"../../static/demo/banner3.jpg",
						type: "text",
						data: "啊啊啊啊啊啊啊啊啊1",
						time: "1598746461",
					},
					{
						isme:true,
						userpic:"../../static/demo/banner3.jpg",
						type: "text",
						data: "啊啊啊啊啊啊啊啊啊2",
						time: "1598746461",
					},
					{
						isme:true,
						userpic:"../../static/demo/banner3.jpg",
						type: "text",
						data: "啊啊啊啊啊啊啊啊啊3",
						time: "1598746461",
					}
				]
			};
		},
		components:{
			chatInput,
			xiaoxiList,
			newsNav
		},
		onLoad(){
			//转化时间
			this.transTime()
			this.pageToBottom()
		},
		methods:{
			//发布
			tapFabu(text){
				console.log("处理信息",text)
				this.xiaoxis=[...this.xiaoxis,...[{
					isme:true,
					userpic:"../../static/demo/banner3.jpg",
					type: "text",
					data: text,
					time: new Date().getTime(),
				}]]
				this.pageToBottom()
			},
			//转换时间
			bijiaoTime(v1,v2){
				return time.gettime.getChatTime(v1,v2)
			},
			transTime(){
				this.xiaoxis.forEach((item,index)=>{
					item.gsTime=this.bijiaoTime(item.time*1,index>0?this.xiaoxis[index-1].time*1:0)
				})
			},
			//查看用户信息
			seeUserInfo(){
				console.log("查看用户信息")
			},
			//返回
			goBack(){
				uni.navigateBack({
					delta:1
				})
			},
			//滚动到底部
			pageToBottom(){
				let query=uni.createSelectorQuery().in(this)
				let itemNode=query.selectAll('.chat_item_top');
				this.$nextTick(()=>{//必须设置$nextTick，否则获取的高度数组为空
					itemNode.fields({
						size:true
					},data=>{
						if(data){
							if(this.isFirst){//第一次进入
								for(let i=0;i<data.length;i++){
									this.xiaoXiHeight+=data[i].height
								}
							}else{
								this.xiaoXiHeight+=data[data.length-1].height
							}
							//滚动到底部
							uni.pageScrollTo({
								scrollTop:this.xiaoXiHeight,
								duration:200
							})
						}else{
							console.log("高度获取错误")
						}
					}).exec()
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.xiaoxi_list{
		box-sizing: border-box;
		padding: 20rpx;
		padding-bottom: 100rpx;
	}
</style>
