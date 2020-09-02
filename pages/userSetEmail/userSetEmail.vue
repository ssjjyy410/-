<template>
	<view class="set_wrapper">
		<view class="tip">
			注意: 密码必须至少包含数字和字母,并且介于8~30位之间
		</view>
		<form @submit="submit">
			<input :disabled="disabled" type="text" name="email" placeholder="输入你要绑定的邮箱" v-model="emailInfo.email"/>
			<input :disabled="disabled" password maxlength="30" name="password" placeholder="请输入密码" v-model="emailInfo.password"/>
			<button
				class="btn"
				:class="{'btn_disable':disabled}" 
				type="primary" 
				size="default"
				form-type="submit"
				:disabled="disabled"
			>完成</button>
		</form>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				disabled: false,//禁止点击或输入
				emailInfo:{
					email:"",
					password:""
				},
			};
		},
		methods:{
			//表单提交
			submit(){
				this.disabled=true;
				uni.showLoading({
					title:"提交中..."
				});
				let {email,password}=this.emailInfo;
				if(!this.checkForm({email,password})){
					this.disabled=false;
					uni.hideLoading();
					return;
				};
				setTimeout(()=>{//模拟异步请求
					console.log(email,password)
					this.disabled=false
					uni.hideLoading()
					uni.showToast({
						duration:1500,
						title:"绑定成功!"
					})
				},3000)
			},
			//表单验证
			checkForm({email,password}){
				// 邮箱格式
				let regexEmail = new RegExp('^[0-9a-zA-Z]+@(([0-9a-zA-Z]+)[.])+[a-z]{2,4}$');
				// 密码格式
				let regexPass = new RegExp('(?=.*[0-9])(?=.*[a-zA-Z]).{8,30}');
				// 输入不能有空格
				let blankPass = /^[^\s]*$/;
				if(email===''||!blankPass.test(email)||!regexEmail.test(email)){
					uni.showToast({
						title:"邮箱格式不正确",
						icon:"none"
					})
					return false;
				}
				if(password===''||!blankPass.test(password)||!regexPass.test(password)){
					uni.showToast({
						title:"密码格式不正确",
						icon:"none"
					})
					return false;
				}
				return true;
			}
		}
	}
</script>

<style lang="less" scoped>
	.set_wrapper{
		box-sizing: border-box;
		padding: 50rpx;
		.tip{
			text-align: center;
			font-size: 25rpx;
			color: #999;
		}
		form{
			input{
				padding: 20rpx;
				border-bottom: 1rpx solid #ccc;
			}
		}
		.btn{
			margin: 40rpx auto;
			width: 90%;
			color: #000;
			background-color: #ffe933;
		}
	}
	.btn_disable{
		color: #999 !important;
		background-color: #eee !important;
	}
</style>
