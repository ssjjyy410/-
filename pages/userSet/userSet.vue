<template>
	<view>
		<xuan-xiang-list :list="list"/>
		<button 
			class="btn" 
			type="primary" 
			size="default"
		>退出登录</button>
	</view>
</template>

<script>
	import xuanXiangList from '../../components/mine/xuanXiangList.vue'
	
	export default {
		data() {
			return {
				list:[
					{icon:"",name:"账号与安全",jumpType:"navigateTo",path:"/pages/userSetPassword/userSetPassword"},
					{icon:"",name:"绑定邮箱",jumpType:"navigateTo",path:"/pages/userSetEmail/userSetEmail"},
					{icon:"",name:"资料编辑",jumpType:"navigateTo",path:"/pages/userSetInfo/userSetInfo"},
					{icon:"",name:"小纸条",jumpType:"switchTab",path:"/pages/paper/paper"},
					{icon:"",name:"清除缓存",jumpType:"",path:""},
					{icon:"",name:"意见反馈",jumpType:"",path:""},
					{icon:"",name:"关于我们",jumpType:"",path:""}
				],//功能选项列表
			};
		},
		components:{
			xuanXiangList
		}
	}
</script>

<style lang="less" scoped>
	.btn{
		margin: 40rpx auto;
		width: 90%;
		color: #000;
		background-color: #ffe933;
	}
</style>
