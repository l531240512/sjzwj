<template>
	<view class="container" :style="{ height: screenHeight }">
		<view style="z-index: 2;">
			<bar :nav="setNav"></bar>
		</view>
	</view>
</template>

<script>
	import bar from "@/components/template/nav/bar.vue"
	export default {
		components:{
				bar
		},
		data() {
			return {
				screenHeight: 0,
				setNav:{
					'bg':'linear-gradient(to right, , )',  //背景色
					// 'bg':'linear-gradient(to right, #74ebd5, #acb6e5)',  //背景色
					'color':'white',  //字体颜色
					'isdisPlayNavTitle': true, //是否显示返回按钮，由于导航栏是共用的，把所有的东西封装好，
					// 然后有些页面不需要的东西通过条件控制进行显示与隐藏
					'navTitle':'' //导航标题
				},
			}
		},
		onLoad() {
			this.screenHeight = uni.getSystemInfoSync().windowHeight
		}
	}
</script>

<style>
	page {
		width: 100%;
		height: 100%;
	}
	.container {
		background: url('https://sjzwj.obs.cn-north-4.myhuaweicloud.com/oss1/1/404/2.jpg') no-repeat center center;
		background-size: 100% 100%;
		width: 100%;
		min-height: 100%;
		background-repeat: no-repeat;
		z-index: 1;
	}

</style>
