<template>
	<view class="info_wrapper">
		<view class="wrapper">
			<view class="usericon_item">
				<view class="title">头像
					<image class="userpic" :src="userpic" mode="aspectFill"></image>
				</view>
				<view class="content">
					<view class="icon iconfont icon-bianji1" @click="chooseUserpic"></view>
				</view>
			</view>
			<view class="usericon_item">
				<view class="title">昵称
					<input @blur="xiugaiUsername" :disabled="disableUsername" class="txt" :class="{'input':disableUsername}" type="text" v-model="username" />
				</view>
				<view class="content">
					<view class="icon iconfont icon-bianji1" @click="tabBianji"></view>
				</view>
			</view>
			<view class="usericon_item">
				<view class="title">性别
					<view class="txt">{{sex}}</view>
				</view>
				<view class="content">
					<view class="icon iconfont icon-bianji1" @click="chooseAction('sex')"></view>
				</view>
			</view>
			<view class="usericon_item">
				<view class="title">生日
					<view class="txt">{{birth}}</view>
				</view>
				<view class="content">
					<picker mode="date" :value="birth" :start="startDate" :end="endDate" @change="bindDateChange">
						<view class="icon iconfont icon-bianji1"></view>
					</picker>
				</view>
			</view>
			<view class="usericon_item">
				<view class="title">情感
					<view class="txt">{{feeling}}</view>
				</view>
				<view class="content">
					<view class="icon iconfont icon-bianji1" @click="chooseAction('feeling')"></view>
				</view>
			</view>
			<view class="usericon_item">
				<view class="title">职业
					<view class="txt">{{job}}</view>
				</view>
				<view class="content">
					<view class="icon iconfont icon-bianji1" @click="chooseAction('job')"></view>
				</view>
			</view>
			<view class="usericon_item">
				<view class="title">家乡
					<view class="txt">{{location}}</view>
				</view>
				<view class="content">
					<picker mode="multiSelector" @change='xiugaiLocation' @columnchange="bindMultiPickerColumnChange" range-key="name" :value="multiIndex" :range="multiLocation">
						<view class="icon iconfont icon-bianji1"></view>
					</picker>
				</view>
			</view>
			<view class="zhezhao" v-if="disabled"></view>
		</view>
		<button
			class="btn" 
			type="primary" 
			size="default"
			:class="{'btn_disable':disabled}" 
			:disabled="disabled"
			@click="submit"
		>提交</button>
	</view>
</template>

<script>
	import location from '@/common/location.js'
	
	export default {
		data() {
			const currentDate = this.getDate({
				format: true
			})
			
			return {
				disabled: false,//是否禁止点击按钮
				userpic:"../../static/demo/2.jpg",
				username:"猪猪ddddddddddddddddddddddddddddddddddddddd",
				disableUsername:true,
				sex:"不限",
				birth:currentDate,
				// disableDate: true,
				feeling:"未婚",
				job:"医生",
				location:"北京市 市辖区",
				multiLocation: [
					location.provinces,
					[location.cities[0]]
				],
				multiIndex:[0,0],
			};	
		},
		computed:{
			startDate() {
				return this.getDate('start');
			},
			endDate() {
				return this.getDate('end');
			}
		},
		methods:{
			//选择头像
			chooseUserpic(){
				uni.chooseImage({
					count:1,
					sizeType:["compressed"],
					success: (res) => {
						this.userpic=res.tempFilePaths[0]
					}
				})
			},
			//允许编辑
			tabBianji(){
				this.disableUsername=!this.disableUsername
			},
			//修改用户名
			xiugaiUsername(e){
				this.username=e.detail.value
				this.tabBianji()
			},
			//选择列表
			chooseAction(state){
				let arr=[]
				switch(state){
					case "sex":
						arr=['不限','男','女'];
						break;
					case "feeling":
						arr=['未婚','已婚'];
						break;
					case "job":
						arr=['医生','老师','律师'];
						break;
					default:
						break;
				}
				uni.showActionSheet({
					itemList:arr,
					success: (res) => {
						let index=res.tapIndex;
						if(state==='sex') this.sex=arr[index];
						if(state==='feeling') this.feeling=arr[index];
						if(state==='job') this.job=arr[index];
					}
				})
			},
			// 获取时间
			getDate(type) {
				const date = new Date();
				let year = date.getFullYear();
				let month = date.getMonth() + 1;
				let day = date.getDate();
	
				if (type === 'start') {
					year = year - 100;
				} else if (type === 'end') {
					year = year;
				}
				month = month > 9 ? month : '0' + month;
				day = day > 9 ? day : '0' + day;
				return `${year}-${month}-${day}`;
			},
			//时间改变
			bindDateChange(e){
				this.birth = e.target.value
			},
			// 选择城市
			bindMultiPickerColumnChange(res){
				let column=res.detail.column
				let row=res.detail.value;
				if(res.detail.column===0){
					let multiLocation=this.multiLocation;
					let code=multiLocation[column][row].code;
					let arr=[];
					location.cities.forEach(item=>{
						if(code===item.provinceCode) arr.push(item)
					})
					this.multiLocation[1]=arr
					this.multiIndex[0]=row
				}else{
					this.multiIndex[1]=row
				}
			},
			//确认修改城市
			xiugaiLocation(e){
				this.multiIndex=e.detail.value
				let multiLocation=this.multiLocation
				let multiIndex=this.multiIndex
				this.location=`${multiLocation[0][multiIndex[0]].name} ${multiLocation[1][multiIndex[1]].name}`
			},
			//提交修改
			submit(){
				this.disabled=true;
				uni.showLoading({
					title:"提交中..."
				});
				setTimeout(()=>{//模拟异步请求
					this.disabled=false
					uni.hideLoading()
					uni.showToast({
						duration:1500,
						title:"修改成功!"
					})
				},3000)
			}
		}
	}
</script>

<style lang="less" scoped>
	.info_wrapper{
		.wrapper{
			position: relative;
			.usericon_item{
				box-sizing: border-box;
				display: flex;
				justify-content: space-between;
				align-items: center;
				padding: 40rpx 0;
				margin: 0 40rpx;
				color: #9b9b9b;
				border-bottom: 1rpx solid #eee;
				white-space: nowrap;
				.title{
					flex: 1;
					display: flex;
					justify-content: space-between;
					align-items: center;
					font-weight: bold;
					.txt{
						max-width: 400rpx;
						color: #000;
						text-overflow: ellipsis;
						overflow: hidden;
						font-weight: normal;
						font-size: 36rpx;
					}
					.input{
						max-width: 150rpx;
					}
					.userpic{
						width: 120rpx;
						height: 120rpx;
						border-radius: 50%;
					}
				}
				.content{
					.icon-bianji1{
						text-align: center;
						margin-left: 20rpx;
						font-size: 50rpx;
					}
				}
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
	.zhezhao{
		position: absolute;
		left: 0;
		right: 0;
		top: 0;
		bottom: 0;
		z-index: 998;
		background-color: hsla(0,0%,0%,0.3);
	}
</style>
