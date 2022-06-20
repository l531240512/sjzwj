<template>
	<view>
		<view class="header" :style="{'height':titleBarHeight,'backgroundImage':nav.bg, 'padding-top':statusBarHeight}">
			<text class="iconfont leftArrow header-back weight"   :style="{'border':nav.color}" v-if="nav.isdisPlayNavTitle" @click="back"> 返回 </text>
			<view class="header-title weight">{{nav.navTitle}}</view>
		</view>
		<view  :style="{'height':titleBarHeight,'padding-top':statusBarHeight}"></view>
	</view>
</template>
<script>
	export default {
		props:["nav"],
		data() {
			return {
				statusBarHeight: 0, 
				titleBarHeight: 0, 
			}
		},
		created() {
			var  that = this;
			 	uni.getSystemInfo({
			 		success: function(res) {
			 			if (res.model.indexOf('iPhone') !== -1) {
							that.titleBarHeight = 44 + 'px';
			 			} else {
			 				that.titleBarHeight = 48  + 'px';
						}
							that.statusBarHeight = res.statusBarHeight  + 'px'
					},
						
			 	})
		 },
		methods: {
			 // 回到上一页
			 back: function(){
				 if(this.nav.isShare){
					uni.switchTab({
						url:'/pages/index/index',
						success: res => {
							// console.log(res);
						},
						fail: (res) => {
							console.log(res)
						},
						complete: () => {}
					})
				 }else{
					 uni.navigateBack({
						delta:1
					 })
				 }
			 },
		}
	}
</script>

<style>
	
	.header {
		display: flex;
		align-items: center;
		top: 0;
		position: fixed;
		width: 100%;
		z-index: 100;
		left:0;
	}
	
	.header .header-title {
		position: absolute;
		left: 50%;
		font-size: 38upx;
		transform: translateX(-50%);
	}
	.header-back{
		position: absolute;
		left:15upx;
		font-size:30upx;
		padding: 10upx;
		border-radius: 50%;
	}
</style>
