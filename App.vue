<script>
	import Vue from 'vue'
	
	export default {
		onLaunch: function() {
			console.log('App Launch')
			// 获取设备信息
			 uni.getSystemInfo({  
				success:function(e){  
					// 获取不同平台的导航栏高度
					// #ifndef MP
					if(e.platform == 'android') {  
						Vue.prototype.customBar = e.statusBarHeight + 50  
					}else {  
						Vue.prototype.customBar = e.statusBarHeight + 45  
					}  
					// #endif  
					// #ifdef MP-WEIXIN  
					let custom = wx.getMenuButtonBoundingClientRect()  
					Vue.prototype.customBar = custom.bottom + custom.top - e.statusBarHeight  
					// #endif
					//获取屏幕高度，在页面中赋值给scroll-view
					Vue.prototype.swiperHeight=e.screenHeight
				}
			})
			
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	@import url("~@/common/icon.css");
	@import url("~@/common/animate.css");
</style>
