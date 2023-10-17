<template>
	<view class="warp">
		<bar :nav="setNav"></bar>
		<view class="myContent">
			<view class="header">
				<image width="100%" height="100%" class="headbgImage" src="https://os01.oss-cn-hangzhou.aliyuncs.com/oss1/1/banner/b1.jpg"></image>
				<image width="100%" height="100%" round class="myPhoto" src="/static/mine/m.svg">
				</image>
				<text class="myInformation">张三</text>
			</view>
			<view class="middle-num">
				<view class="oner">
					<view class="zi">
						<text class="zier">{{coupon}}<text class="zisan">张</text></text>
						<text class="quan">优惠券</text>
					</view>
				</view>
				<view class="twoer">|</view>
				<view class="three">
					<view class="zi">
						<text class="zier">{{integral}}\n</text>
						<text class="quan">积分</text>
					</view>
				</view>
			</view>
			<view class="mydingdan">
				<view class="zhifu">
					<uni-grid :column="5" class="uniGrid">
						<uni-grid-item v-for="(item, index) in icon" :index="index" :key="key" >
							<view class="uniGridItem">
								<uni-badge class="uni-badge-left-margin" :text="item.count" absolute="rightTop" size="small">
									<uni-icons custom-prefix="iconfont" :type="item.photoSrc" :size="30" @click="toUrl(item.toUrl)"/>
								</uni-badge>
								<text class="text">{{item.text}}</text>
							</view>
						</uni-grid-item>
					</uni-grid>
				</view>
			</view>
			<view class="liebiao">
				<cell v-for="(liebiao,key) in lbIcon" :key="key">
				  <view class="uniCellItem">
					  <uni-icons :type="liebiao.photoSrc" :size="30" @click="toUrl(liebiao)" />
					  <text class="text">{{liebiao.text}}</text>
				  </view>
				</cell>
			</view>
		</view>
	</view>
</template>
 
<script>
	import bar from "@/components/template/nav/bar.vue"
	import uniIcons from "@/components/uni-icons/uni-icons.vue"
	import uniBadge from "@/components/template/uni-badge/uni-badge.vue"
	export default {
		components:{
				bar,uniIcons,uniBadge
		},
		data() {
			return {
				coupon: 6,
				integral: 300,
				icon: [],
				setNav:{
					'bg':'linear-gradient(to right, #FFFFFF, #FFFFFF)',  //背景色
					'color':'white',  //字体颜色
					'isdisPlayNavTitle':false, //是否显示返回按钮，由于导航栏是共用的，把所有的东西封装好，
					'navTitle':'我的' //导航标题
				},
				lbIcon:[]
			}
		},
		onLoad() {
			this.init()
			//支付导航
			this.tabBarIcon();
			//列表单元格
			this.liebiaoIcon();
 
		},
		methods: {
			init() {
				uni.request({
				    url: 'https://os01.oss-cn-hangzhou.aliyuncs.com/oss1/1/m/m.json', //仅为示例，并非真实接口地址。
				    success: (res) => {
						this.coupon = res.data.coupon
						this.integral = res.data.integral
						let iconCountList = res.data.iconCountList
						this.icon.forEach( (icon, index) => {
							icon.count = iconCountList[icon.index]
						})
				    },
				    fail: (err) => { //失败操作
				    }
				});
			},
			/* 支付导航 */
			tabBarIcon() {
				var data = {
					"icons": [{
							"index": 0,
							"photoSrc": 'icon-daifukuan',
							"count": '',
							"text": "待付款",
							"toUrl": "/pages/error/index"
						},
						{
							"index": 1,
							"photoSrc": 'icon-daifahuo',
							"count": '',
							"text": "待发货",
							"toUrl": "/pages/error/index"
						},
						{
							"index": 2,
							"photoSrc": "icon-daishouhuo",
							"count": '',
							"text": "待收货",
							"toUrl": "/pages/error/index"
						},
						{
							"index": 3,
							"photoSrc": "icon-dingdanwancheng",
							"count": '',
							"text": "已完成",
							"toUrl": "/pages/error/index"
						},
						{
							"index": 4,
							"photoSrc": "icon-shouhoufuwu",
							"count": '',
							"text": "售后",
							"toUrl": "/pages/error/index"
						}
					]
				};
				this.icon = data.icons
			},
			toUrl(item) {
				if(item.text == '客服电话'){
					uni.makePhoneCall({
						phoneNumber: '15047690961'
					});
					return
				}
				uni.navigateTo({
				    url: item.toUrl,
				    success: res => {
				
				    },
				    fail: (e) => {console.log(e)},
				    complete: () => {}
				});
			},
			//列表单元格
			liebiaoIcon() {
				var data = {
					"icons": [{
							"photoSrc": "star-filled",
							"text": "我的收藏",
							"toUrl": "/pages/error/index"
						},
						{
							"photoSrc": "location-filled",
							"text": "地址管理",
							"toUrl": "/pages/error/index"
						},
						{
							"photoSrc": "contact-filled",
							"text": "关于我们",
							"toUrl": "/pages/tool/map"
						},
						{
							"photoSrc": "phone-filled",
							"text": "客服电话",
							"toUrl": "/pages/error/index"
						}
					]
				};
				this.lbIcon = data.icons
			}
		}
	}
</script>
 
<style>
	page {
		background: #eaeaea;
	}
 
	.myContent {
		width: 100%;
		height: 100%;
		margin: 0 auto;
	}
 
	.header {
		flex-direction: row;
		display: flex;
		height: 200rpx;
	}
 
	.headbgImage {
		height: 25%;
		width: 100%;
		position: absolute;
		z-index: 1;
	}
 
	.myPhoto {
		height: 90rpx;
		width: 90rpx;
		position: absolute;
		z-index: 2;
		margin-left: 3%;
		margin-top: 3%;
	}
 
	.myInformation {
		position: absolute;
		z-index: 2;
		margin-left: 16%;
		margin-top: 7%;
	}
 
	.middle-num {
		position: absolute;
		z-index: 2;
		display: flex;
		flex-wrap: nowrap;
		background: white;
		width: 95%;
		margin-left: 20rpx;
		height: 160rpx;
		border-radius: 10px;
		margin-top: -50rpx;
	}
 
	.oner {
		flex-grow: 1;
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100%;
	}
 
	.twoer {
		flex-grow: 1;
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100%;
		color: #eaeaea;
	}
 
	.three {
		flex-grow: 1;
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100%;
	}
 
	.zier {
		font-size: 48rpx;
		color: #333333;
	}
 
	.zisan {
		font-size: 24rpx;
		color: #333333;
	}
 
	.quan {
		font-size: 24rpx;
		color: #999999;
	}
 
	.zi {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
 
	.mydingdan {
		display: flex;
		flex-wrap: nowrap;
		background: #fff;
		width: 95%;
		height: 250rpx;
		margin-left: 20rpx;
		border-radius: 10px;
		margin-top: 130rpx;
		flex-direction: column;
	}
 
	.mydingdan .row1 .cell {
		position: inherit;
		border-radius: 10px 10px 0px 0px;
	}
 
	.zhifu {
		margin-top: 5rpx
	}
	
	.uniGrid{
		display: flex;
		justify-content: space-around;
		margin-top: 10%;
		margin-bottom: 10%;
	}
	
	.uniGridItem{
		display: flex;
		flex-direction: column;
	}
 
	.liebiao {
		display: flex;
		justify-content: space-around;
		height: 658rpx;
		background: #fff;
		width: 91%;
		border-radius: 10px;
		padding: 2%;
		margin: 20rpx 20rpx 10rpx 20rpx;
	}
	.liebiao .cell{
		height: 16%;
	}
	.uniCellItem{
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
		margin-top: 50rpx;
	}
</style>