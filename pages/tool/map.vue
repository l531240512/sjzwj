<template>
	<view>
		<bar :nav="setNav"></bar>
		<view style="height: 100upx;">
			<view style="margin-left: 50upx; margin-top: 50upx; font-size:32upx; font-weight:bold; letter-spacing:2upx;">
				<text class="flex flex-direction">赤峰市敖汉旗宝老线玉卿小学西南侧约100米</text>
			</view>
			<view style="margin-left: 50upx; margin-top: 20upx; color:darkgrey">
				<image src="https://sjzwj.obs.cn-north-4.myhuaweicloud.com/oss1/1/h.jpg"></image>
			</view>
		</view>
		<view style="height: 550upx;"></view>
		<view class="page-body">
			<view class="page-section page-section-gap">
				<map style="width: 100%; height: 300px;" :latitude="latitude" :longitude="longitude" :markers="covers">
				</map>
			</view>
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
			id: 0,
			title: 'map',
			latitude: 41.828508,
			longitude: 120.09356,
			covers: [{
				id: 1,
				latitude: 41.828508,
				longitude: 120.09356,
				iconPath: '../../static/1.svg'
			}, {
				id: 2,
				latitude: 41.828508,
				longitude: 120.09356,
				iconPath: '../../static/1.svg'
			}],
			setNav:{
				'bg':'linear-gradient(to right, #FFFFFF, #FFFFFF)',  //背景色
				'color':'white',  //字体颜色
				'isdisPlayNavTitle': true, //是否显示返回按钮，由于导航栏是共用的，把所有的东西封装好，
				'navTitle':'关于我们' //导航标题
			},
		}
	},
	methods: {

	}
}
</script>

<style>
</style>
