<template>
	<view class="warp">
		<bar :nav="setNav"></bar>
		<view class="uni-padding-wrap">
			<view class="page-section swiper">
				<view class="page-section-spacing">
					<swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
						<swiper-item>
							<view class="swiper-item">
								<image src="https://os01.oss-cn-hangzhou.aliyuncs.com/oss1/1/banner/b1.jpg"></image>
							</view>
						</swiper-item>
						<swiper-item>
							<view class="swiper-item">
								<image src="https://os01.oss-cn-hangzhou.aliyuncs.com/oss1/1/banner/b2.jpg"></image>
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
		<view style="height: 50upx;"></view>
		<view style="display: flex; justify-content:center; align-items:center; flex-direction: column;">
			<!-- uni-grid 的颜色溢出，如果给父级view设置圆角会失效，所以给uni-grid父级view添加overflow：hidden，uni-grid 的颜色不会溢出，uni-grid的圆角可以正常显示 -->
			<uni-card :is-shadow="true" is-full=true style="overflow: hidden; width: 95%; border-radius:30upx;">
				<view>
					<uni-grid :column="8" style="background-color: #fff; display: flex; flex-direction: row;">
						<uni-grid-item v-for="(item, index) in menuList1" :index="index" :key="index" >
							<view style="margin-top: 20upx;" @tap="goPage(item.idx)">
								<image :src="item.img" ></image>
							</view>
							<view style="align-content: center;">
								<text class="text">{{item.name}}</text>
							</view>
						</uni-grid-item>
					</uni-grid>
				</view>
				<view>
					<uni-grid :column="8" style="background-color: #fff; display: flex; flex-direction: row;">
						<uni-grid-item v-for="(item, index) in menuList2" :index="index" :key="index" >
							<view style="margin-top: 20upx;" @tap="goPage(item.idx)">
								<image :src="item.img" ></image>
							</view>
							<view style="align-content: center; margin-bottom : 20upx;">
								<text class="text" style="align-content: center;">{{item.name}}</text>
							</view>
						</uni-grid-item>
					</uni-grid>
				</view>
			</uni-card>
		</view>
		<view style="height: 50upx;"></view>
		<view style="background-color: #fff; display: flex; flex-direction: column; align-items:center; width: 750upx;">
		<view @tap="goPage('new')" style="display: flex; flex-direction: row; align-items:center; height: 220upx; width: 750upx;">
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
		<!-- <view style="height: 50upx;"></view> -->
		<view @tap="goPage('new')" style="display: flex; flex-direction: row; align-items:center; height: 220upx; width: 750upx;">
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
		</view>
		<view style="height: 50upx;"></view>
	</view>
</template>

<script>
	import bar from "@/components/template/nav/bar.vue"
	import uniCard from "@/components/uni-card/uni-card.vue"
	export default {
		components:{
				bar, uniCard
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
					'bg':'linear-gradient(to right, #FFFFFF, #FFFFFF)',  //背景色
					// 'bg':'linear-gradient(to right, #74ebd5, #acb6e5)',  //背景色
					'color':'white',  //字体颜色
					'isdisPlayNavTitle':false, //是否显示返回按钮，由于导航栏是共用的，把所有的东西封装好，
					// 然后有些页面不需要的东西通过条件控制进行显示与隐藏
					'navTitle':'五金三十年老店' //导航标题
				},
				renderImage: false,
				goodsTabData: [{
					tag:"tag111",
				},
				{
					tag:"tag2",
				}],
				menuList1:[
					{
						name:'农机具',
						id: '1',
						idx: 0,
						img:'/static/nj.svg'
					},
					{
						name:'工具包',
						id: '2',
						idx: 1,
						img:'/static/gj.svg'
					},
					{
						name:'插排',
						id: '3',
						idx: 2,
						img:'/static/cz.svg'
					},
					{
						name:'水管',
						id: '4',
						idx: 3,
						img:'/static/sg.svg'
					}
				],
				menuList2:[
					{
						name:'家具',
						id: '5',
						idx: 4,
						img:'/static/jj.svg'
					},
					{
						name:'服饰',
						id: '6',
						idx: 5,
						img:'/static/fs.svg'
					},
					{
						name:'化妆品',
						id: '7',
						idx: 6,
						img:'/static/hzp.svg'
					},
					{
						name:'肉禽',
						id: '8',
						idx: 7,
						img:'/static/rq.svg'
					}
				],
				imageURL: '/static/11.png'
			}
		},
		onLoad() {
			// tabBar 角标数字
			// uni.setTabBarBadge({ //显示数字
			//   index: 1,//tabbar下标
			//   text: '1'//数字
			// })
		},
		onShareAppMessage() {
			return {
			  title: '自定义分享标题',
			  path: 'pages/index/index'
			}
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
				if(e === 'new'){
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
				}else if(e === '3'){
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
				}
				else{
					uni.setStorageSync('idx', e);
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
				// 从聊天记录中选择文件
				// wx.chooseMessageFile({
				//   count: 10,
				//   type: 'all',
				//   success (res) {
				//     // tempFilePath可以作为 img 标签的 src 属性显示图片
				//     const tempFilePaths = res.tempFiles
				//   }
				// })
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
		width: 70upx;
		height: 70upx;
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
