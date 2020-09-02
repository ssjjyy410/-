<template>
	<view class="commentW">
		<comment-list :list="list" @isShowReply="isShowReply"/>
		<view class="reply" v-show="isShow">
			<template v-for="(item,index1) in list.reply">
				<comment-list :list="item" :key="index1"/>
			</template>
		</view>
	</view>
</template>

<script>
	import commentList from './commentList.vue'
	
	export default {
		data() {
			return {
				isShow: false, //是否显示回复列表
			};
		},
		props:["list"],
		components:{
			commentList
		},
		methods:{
			//是否显示回复列表
			isShowReply(){
				console.log("aaa")
				this.isShow=!this.isShow
			}
		}
	}
</script>

<style lang="less" scoped>
	.commentW{
		.reply{
			padding: 20rpx;
			margin-left: 100rpx;
			background-color: #f4f4f4;
		}
	}
</style>
