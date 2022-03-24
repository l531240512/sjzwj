<template>
	<view class="warp">
		<bar :nav="setNav"></bar>
		<view class="uni-padding-wrap">
			<view class="page-section swiper">
				<view class="page-section-spacing">
					<swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
						<swiper-item>
							<view class="swiper-item">
								<image src="https://os01.oss-cn-hangzhou.aliyuncs.com/oss1/1/sjz.png"></image>
							</view>
						</swiper-item>
						<swiper-item>
							<view class="swiper-item">
								<image src="/static/1.jpeg"></image>
							</view>
						</swiper-item>
					</swiper>
				</view>
			</view>
		</view>
		<view class="content">
			<view class="text-area">
				<text class="title">{{title}}</text>
			</view>
			<view>
				<button type="primary" class="btn2" size="mini" plain="true" @tap="CallPhone('15047690961')">联系电话：150 4769 0961</button>
			</view>
		</view>
		<view>
			<uni-grid :column="8" style="background-color: #fff; display: flex; flex-direction: row;">
			    <uni-grid-item>
					<view>
						<view @tap="goPage('1')">
							<image src="/static/nj.svg" height="20upx" width="20upx"></image>
						</view>
						<view style="align-content: center;">
							<text class="text">农机具</text>
						</view>
					</view>
			    </uni-grid-item>
			    <uni-grid-item>
					<view @tap="goPage('1')">
						<image src="/static/gj.svg" height="20upx" width="20upx"></image>
					</view>
					<view style="align-content: center;">
						<text class="text">工具包</text>
					</view>
			    </uni-grid-item>
			</uni-grid>
		</view>
		<view>
			<uni-grid :column="8" style="background-color: #fff; display: flex; flex-direction: row;">
			    <uni-grid-item>
					<view @tap="goPage('1')">
						<image src="/static/cz.svg" height="20upx" width="20upx"></image>
					</view>
					<view style="text-align: center;">
						<text class="text">插排</text>
					</view>
			    </uni-grid-item>
				<uni-grid-item>
					<view @tap="goPage('1')">
						<image src="/static/sg.svg" height="20upx" width="20upx"></image>
					</view>
					<view style="align-content: center;">
						<text class="text">水管</text>
					</view>
				</uni-grid-item>
			</uni-grid>
		</view>
		<view style="height: 50upx;"></view>
		<view @tap="goPage('2')" style="background-color: #fff; display: flex; flex-direction: row; align-items:center; height: 220upx; width: 750upx;">
			<view style="flex-grow: 2;">
				<view style="margin-left: 50upx;">
					<text class="flex flex-direction">内蒙古赤峰市敖汉旗四家子镇</text>
				</view>
				<view style="margin-left: 50upx; margin-top: 20upx; color:darkgrey">
					<text class="flex flex-direction">时间：2022-1-1</text>
				</view>
			</view>
			<view style="flex-grow: 1;">
				<image style="height: 160upx; width: 200upx;border-radius:10upx" src="https://os01.oss-cn-hangzhou.aliyuncs.com/oss1/1/sjz1.png" data-src="/static/1.svg"></image>
			</view>
		</view>
		<view style="height: 50upx;"></view>
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
				title: '地址：敖汉旗四家子镇四家子村邮局斜对面',
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500,
				// 自定义导航栏对象
				setNav:{
					'bg':'linear-gradient(to right, #74ebd5, #acb6e5)',  //背景色
					'color':'white',  //字体颜色
					'isdisPlayNavTitle':false, //是否显示返回按钮，由于导航栏是共用的，把所有的东西封装好，
					// 然后有些页面不需要的东西通过条件控制进行显示与隐藏
					'navTitle':'五金' //导航标题
				},
				renderImage: false,
				goodsTabData: [{
					tag:"tag111",
				},
				{
					tag:"tag2",
				}],
				imageURL: '/static/11.png'
			}
		},
		onLoad() {
		},
		onShareAppMessage() {
			uni.share({
				provider: "weixin",
				scene: "WXSceneSession",
				type: 1,
				summary: "赶紧跟我一起来体验！",
				success: function (res) {
					console.log("success:" + JSON.stringify(res));
				},
				fail: function (err) {
					console.log("fail:" + JSON.stringify(err));
				}
			});
		},
		methods: {
			change(e) {
				let {
					index
				} = e.detail
				this.list[index].badge && this.list[index].badge++
			
				uni.showToast({
					title: `点击第${index+1}个宫格`,
					icon: 'none'
				})
			},
			goPage(e) {
				if(e === '2'){
					var url = "/pages/new/index";
					uni.navigateTo({
					    url: url,
					    success: res => {
							console.log(res);
					    },
					    fail: (res) => {
							console.log(res);
						},
					    complete: () => {}
					});
				}else{
					var url = "/pages/goods/shop";
					uni.switchTab({
						url:url,
						success: res => {
							// console.log(res);
						},
						fail: (res) => {
							// console.log(res);
						},
						complete: () => {}
					})
				}
			},
			previewImg(logourl) {
				let _this = this;
				let imgsArray = [];
				imgsArray[0] = logourl
				uni.previewImage({
					current: 0,
					urls: imgsArray
				});
			},
			/*拨打电话*/
			CallPhone(e){
			    uni.makePhoneCall({
					phoneNumber: e
				});
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 350rpx;
		width: 600rpx;
		margin-top: 80rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}
	.button {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}
	
	.text-area {
		display: flex;
		justify-content: center;
		margin: 36rpx 36rpx;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
	
	uni-swiper .uni-swiper-dot {
		display:inline-block;
		width:14px!important;
		height:4px!important;
		cursor:pointer;
		-webkit-transition-property:background-color;
		transition-property:background-color;
		-webkit-transition-timing-function:ease;
		transition-timing-function:ease;
		background:rgba(255,255,255,.3);
		border-radius:5px!important
	}
	
	uni-swiper .uni-swiper-dot-active {
	width:20px!important;
	background-color:#fff!important;
	}
	
	swiper-item image{
		width: 100%;
	}
	
	.zaiui-goods-tab-box {
		position: sticky;
		padding: 2rpx 0;
		transition: all .25s;
		z-index: 9999;
		background: #fff;
	
		/* #ifndef MP */
		top: calc(var(--status-bar-height) + 101rpx);
		/* #endif */
	
		/* #ifdef MP */
		top: calc(var(--status-bar-height) + 161rpx);
		/* #endif */
	}
	
	.btn2{
		border-radius: 17px;
	}
	.grid-item-box {
		flex: 1;
		// position: relative;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 15px 0;
	}
	
	.grid-item-box-row {
		flex: 1;
		// position: relative;
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: center;
		padding: 15px 0;
	}
	
	uni-grid-item image{
		width: 200upx;
		height: 200upx;
		margin: auto;
	}
	
	uni-grid-item view{
		display: flex;
		flex-wrap: wrap;
		flex-direction: column;
	}
	
	uni-grid uni-grid-item{
		flex: 1;
	}
	
	uni-grid-item view text{
		align-content: center;
	}
</style>
