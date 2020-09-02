<template>
	<view>
		<uni-nav-bar 
			statusBar 
			:border="false"
			backgroundColor="#ffe933"
			leftIcon="closeempty"
			leftSize="40"
			@clickLeft="jumpBack"
		>
		</uni-nav-bar>
		<!-- 背景图 -->
		<image class="bgimg" src="../../static/common/loginhead.png" mode="widthFix"></image>
		<view class="set_wrapper">
			<!-- 登录框 -->
			<form>
				<template v-if="isShowAvatar">
					<view class="pass_wrapper">
						<view class="location">+86</view>
						<input :disabled="disabled" type="text" maxlength="18" name="phonenumber" placeholder="输入手机号码" v-model="phonenumber" key="phonenumber"/>
					</view>
					<view class="avatar_wrapper">
						<input :disabled="disabled" maxlength="4" name="avatar" placeholder="请输入验证码" v-model="avatar" key="avatar"/>
						<view class="getavatar" @click="getAvatar" :class="{'avatar_disable':codetime>0}">{{codetime<=0?"获取验证码":`倒计时${codetime}`}}</view>
					</view>
				</template>
				<template v-else>
					<view class="one_wrapper">
						<input :disabled="disabled" type="text" maxlength="30" name="inputOne" placeholder="昵称/手机号/邮箱" v-model="username" key="username"/>
					</view>
					<view class="pw_wrapper">
						<input :disabled="disabled" maxlength="30" name="password" placeholder="请输入密码" v-model="password" key="password"/>
						<view class="forget">忘记密码?</view>
					</view>
				</template>
				<button
					class="btn"
					:class="{'btn_disable':disabled}" 
					type="primary" 
					size="default"
					:disabled="disabled"
					@click="submit"
				>登录</button>
			</form>
			<!-- 账号密码登陆 -->
			<view class="nologin_tologin" @click="toggleForm">{{isShowAvatar?'账号密码登录 ':'验证码登录 '}}<view>></view></view>
			<!-- 第三方登录 -->
			<view class="nologin_third_tip">---- 第三方登录 ----</view>
			<no-login/>
			<view class="xieyi_tip">注册及代表您同意<view class="xieyi">《糗事百科用户协议》</view></view>
		</view>
	</view>
</template>

<script>
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue"
	import noLogin from '@/components/mine/noLogin.vue'
	
	export default {
		data() {
			return {
				disabled:false,//是否禁用按钮
				isShowAvatar:false,//是否验证码登录
				phonenumber:"",//电话号码
				avatar:"",//验证码
				username:"",//昵称/手机号/邮箱
				password:"",//密码
				codetime:0,//验证码获取倒计时
			}
		},
		components:{
			uniNavBar,
			noLogin
		},
		methods: {
			//获取验证码
			getAvatar(){
				if(this.disabled) return;
				if(!this.checkPhone(this.phonenumber)) return;
				if(this.codetime>0){
					uni.showToast({
						title:"无法重复获取",
						icon:"none"
					})
					return;
				};
				//获取验证码
				
				//获取成功,倒计时
				this.codetime=60;
				this.timer=setInterval(()=>{
					--this.codetime
					if(this.codetime<=0) clearInterval(this.timer)
				},1000)
			},
			//切换登录表单
			toggleForm(){
				if(this.disabled) return;
				this.phonenumber=''
				this.avatar=''
				this.username=''
				this.password=''
				this.isShowAvatar=!this.isShowAvatar
			},
			//返回
			jumpBack(){
				if(this.disabled) return;
				uni.navigateBack({
					delta: 1
				});
			},
			//表单提交
			submit(){
				this.disabled=true;
				uni.showLoading({
					title:"提交中..."
				});
				
				let phonenumber=this.phonenumber,
					avatar=this.avatar,
					username=this.username,
					password=this.password;
				
				if(this.isShowAvatar&&!this.checkAvatarForm({avatar,phonenumber})){
					console.log(avatar,phonenumber)
					this.disabled=false;
					uni.hideLoading();
					return;
				}
				if(!this.isShowAvatar&&!this.checkLoginForm({username,password})){
					console.log(username,password)
					this.disabled=false;
					uni.hideLoading();
					return;
				}
				
				setTimeout(()=>{//模拟异步请求
					console.log("请求中...")
					this.disabled=false
					uni.hideLoading()
					uni.showToast({
						duration:1500,
						title:"登录成功!"
					})
				},3000)
			},
			// 验证手机号码
			checkPhone(phonenumber){
				let regexPhone = /^1(3|4|5|6|7|8|9)\d{9}$/;
				// 输入不能有空格
				let blankPass = /^[^\s]*$/;
				if(phonenumber===''||!blankPass.test(phonenumber)||!regexPhone.test(phonenumber)){
					uni.showToast({
						title:"电话号码格式不正确",
						icon:"none"
					})
					return false;
				}
				return true;
			},
			//验证码表单验证
			checkAvatarForm({avatar,phonenumber}){
				// 电话格式
				let regexPhone = /^1(3|4|5|6|7|8|9)\d{9}$/;
				// 输入不能有空格
				let blankPass = /^[^\s]*$/;
				if(!this.checkPhone(phonenumber)) return;
				if(avatar===''||!blankPass.test(avatar)){
					uni.showToast({
						title:"验证码不正确",
						icon:"none"
					})
					return false;
				}
				return true;
			},
			//登录表单验证
			checkLoginForm({username,password}){
				// 密码格式
				let regexPass = new RegExp('(?=.*[0-9])(?=.*[a-zA-Z]).{8,30}');
				// 输入不能有空格
				let blankPass = /^[^\s]*$/;
				if(username===''||!blankPass.test(username)){
					uni.showToast({
						title:"昵称/手机号/邮箱格式不正确",
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
			},
			
		},
		onUnload(){
			if(!this.timer) clearInterval(this.timer);
		}
	}
</script>

<style lang="less" scoped>
	.bgimg{
		width: 100%;
	}
	.set_wrapper{
		box-sizing: border-box;
		padding: 50rpx;
		form{
			input{
				padding: 20rpx;
				border-bottom: 1rpx solid #ccc;
			}
			.pass_wrapper{
				position: relative;
				input{
					padding-left: 100rpx;
				}
				.location{
					position: absolute;
					left: 0;
					top: 0;
					width: 100rpx;
					height: 100%;
					line-height: 85rpx;
					font-size: 35rpx;
					text-align: center;
				}
			}
			.avatar_wrapper{
				position: relative;
				input{
					padding-right: 180rpx;
				}
				.getavatar{
					box-sizing: border-box;
					position: absolute;
					right: 0;
					top: 10%;
					width: 180rpx;
					height: 80%;
					color: #939393;
					background-color: #ffe933;
					border-radius: 10rpx;
					text-align: center;
					font-size: 30rpx;
					padding: 11rpx;
				}
				.avatar_disable{
					background-color: #f4f4f4;
				}
			}
			.pw_wrapper{
				position: relative;
				input{
					padding-right: 180rpx;
				}
				.forget{
					position: absolute;
					right: 0;
					top: 26%;
					font-size: 32rpx;
					text-align: center;
					width: 180rpx;
				}
			}
		}
		.btn{
			margin: 40rpx auto;
			width: 90%;
			color: #000;
			background-color: #ffe933;
		}
		.nologin_tologin{
			position: relative;
			display: inline-block;
			left: 50%;
			transform: translateX(-50%);
			margin-bottom:40rpx;
			text-align: center;
			font-size: 30rpx;
			color: #343434;
			view{
				color: #dcdcdc;
				display: inline-block;
			}
		}
		.nologin_third_tip{
			position: relative;
			text-align: center;
			color: #9b9b9b;
			font-size: 30rpx;
			width: 100%;
		}
		.nologin_third{
			margin: 30rpx 0;
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
		.xieyi_tip{
			text-align: center;
			font-size: 25rpx;
			color: #9b9b9b;
			.xieyi{
				display: inline-block;
				color: #2baefc;
			}
		}
	}
	.btn_disable{
		color: #999 !important;
		background-color: #eee !important;
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
