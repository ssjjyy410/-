<template>
	<view class="nologin_third">
		<view 
			class="icon iconfont"
			hover-class="active"
			v-for="(item,index) in provider"
			:class="item.icon"
			:key="index"
			@click="otherLogin(item)"
		></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				provider:[]
			};
		},
		methods:{
			//第三方登录
			otherLogin(item){
				uni.login({
				  provider: item.name,
				  success: function (loginRes) {
				    console.log("登录",loginRes.authResult);
				  }
				});
			}
		},
		created(){
			let that=this
			//获取登录信息
			uni.getProvider({
				service:'oauth',
				success: (res) => {
					let provider=res.provider
					let arr=[]
					console.log(res)
					provider.forEach(item=>{
						switch(item){
							case "weixin":
								arr.push({name:"weixin",icon:"icon-weixin"})
								break;
							case "qq":
								arr.push({name:"qq",icon:"icon-QQ"})
								break;
							case "sinaweibo":
								arr.push({name:"sinaweibo",icon:"icon-xinlangweibo"})
								break;
							default:
								break;
						}
					})
					that.provider=arr
				}
			})
			
		}
	}
</script>

<style lang="less" scoped>
	.nologin_third{
		margin: 40rpx 0;
		padding: 0 40rpx;
		display: flex;
		justify-content: space-around;
		.icon{
			font-size: 55rpx;
			text-align: center;
			color: #fff;
			flex: 120rpx 0 0;
			line-height: 120rpx;
			border-radius: 50%;
		}
		.icon-weixin{
			background-color: #2bd19b;
		}
		.icon-QQ{
			background-color: #2acefc;
		}
		.icon-xinlangweibo{
			background-color: #fc7729;
		}
	}
	.active{
		color: #fff;
		position: relative;
		&::before{
			position: absolute;
			content: "";
			left: 0;
			top: 0;
			bottom: 0;
			right: 0;
			border-radius: 50%;
			background-color: hsla(0%,0%,0%,.01);
			opacity: 0.2;
		}
	}
</style>
