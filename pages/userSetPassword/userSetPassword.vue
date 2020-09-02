<template>
	<view class="set_wrapper">
		<view class="tip">
			注意: 密码必须至少包含数字和字母,并且介于8~30位之间
		</view>
		<form @submit="submit">
			<input :disabled="disabled" password maxlength="30" name="oldpassword" placeholder="输入旧密码" v-model="pass.oldpassword"/>
			<input :disabled="disabled" password maxlength="30" name="newpassword" placeholder="输入新密码" v-model="pass.newpassword"/>
			<input :disabled="disabled" password maxlength="30" name="renewpassword" placeholder="输入确认密码" v-model="pass.renewpassword"/>
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
				pass:{
					oldpassword:"",
					newpassword:"",
					renewpassword:""
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
				let {oldpassword,newpassword,renewpassword}=this.pass;
				if(!this.checkForm({oldpassword,newpassword,renewpassword})){
					this.disabled=false;
					uni.hideLoading();
					return;
				};
				setTimeout(()=>{//模拟异步请求
					console.log(oldpassword,newpassword,renewpassword)
					this.disabled=false
					uni.hideLoading()
					uni.showToast({
						duration:1500,
						title:"修改成功!"
					})
				},3000)
			},
			//表单验证
			checkForm({oldpassword,newpassword,renewpassword}){
				// 密码至少包含数字和字母
				let regexPass = new RegExp('(?=.*[0-9])(?=.*[a-zA-Z]).{8,30}');
				//密码不能有空格
				let blankPass = /^[^\s]*$/;
				if(oldpassword===''||!blankPass.test(oldpassword)||!regexPass.test(oldpassword)){
					uni.showToast({
						title:"旧密码格式不正确",
						icon:"none"
					})
					return false;
				}
				if(newpassword===''||!blankPass.test(newpassword)||!regexPass.test(newpassword)){
					uni.showToast({
						title:"新密码格式不正确",
						icon:"none"
					})
					return false;
				}
				if(renewpassword===''||!blankPass.test(renewpassword)||!regexPass.test(renewpassword)){
					uni.showToast({
						title:"确认密码格式不正确",
						icon:"none"
					})
					return false;
				}
				if(newpassword!==renewpassword){
					uni.showToast({
						title:"新密码与确认密码要相同",
						icon:"none"
					})
					return false;
				}
				return true;
			},
			
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
