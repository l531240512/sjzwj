<template>
	<view class="uni-container">
		<bar :nav="setNav"></bar>
		<view>
			<image class="imageWidth" @click="previewImg(product.image)" data-src="/static/tmp/22.png" :src=product.image ></image>
		</view>
		<view style="background-color: #fff;">
			<view>
				<p style="margin-left: 30upx; margin-right: 30upx; padding-top: 30upx;">
					<text style="font-size: 33upx;">{{product.title}}</text>
				</p>
			</view>
			<view>
				<p style="margin-top: 30upx;margin-left: 25upx;padding-bottom: 30upx;color: orangered;">
					￥<text style="font-size:initial; ">{{product.price}}</text>
				</p>
			</view>
		</view>
		<view style="height: 30upx;"></view>
		<view style="background-color: #fff;">
			<p style="padding: auto; font-size: 32upx;">
				<button @tap="CallPhone('15047690961')">三十年老店,联系电话：{{phone}}</button>
			</p>
		</view>
		<view style="height: 30upx;"></view>
		<uni-section title="商品信息" type="line">
			<view class="uni-padding-wrap uni-common-mt">
				<uni-segmented-control :current="current" :values="items" :style-type="styleType"
					:active-color="activeColor" @clickItem="onClickItem" />
			</view>
			<view class="content">
				<view v-if="current === 0">
					<image @click='previewImg(product.image)' data-src='/static/tmp/22.png' :src=product.image ></image>
				</view>
				<view v-if="current === 1"><text class="content-text">商品参数</text></view>
				<view v-if="current === 2">
					<!-- <textarea class="textarea" v-model="txt" placeholder="暂时不支持评论"></textarea> -->
					<button type="primary" disabled="true" @tap="submit1()">提交</button>
				</view>
			</view>
		</uni-section>
		<view class="goods-carts">
			<uni-goods-nav :options="options" :fill="true" :button-group="buttonGroup" @click="onClick"
				@buttonClick="buttonClick" />
		</view>
		<view style="height: 500upx;"></view>
	</view>
</template>

<script>
	import bar from "@/components/template/nav/bar.vue"
	import uniCard from "@/components/uni-card/uni-card.vue"
	import uniGoodsNav from "@/components/uni-goods-nav/uni-goods-nav.vue"
	import uniSection from "@/components/uni-section/uni-section.vue"
	import uniSegmentedControl from "@/components/uni-segmented-control/uni-segmented-control.vue"
	export default {
		components:{
				bar, uniCard, uniGoodsNav, uniSection, uniSegmentedControl
		},
		data() {
			return {
				// 自定义导航栏对象
				setNav:{
					'bg':'linear-gradient(to right, #FFFFFF, #FFFFFF)',  //背景色
					'color':'white',  //字体颜色
					'isdisPlayNavTitle':true, //是否显示返回按钮，由于导航栏是共用的，把所有的东西封装好，
					'isShare':false, 
					// 然后有些页面不需要的东西通过条件控制进行显示与隐藏
					'navTitle':'标题' //导航标题
				},
				isShow1:true,
				isShow2:false,
				isShow3:false,
				productId: 0,
				txt: '',
				phone: '150 4769 0961',
				product:{},
				options: [{
					icon: 'chat',
					text: '客服'
				}
				],
				buttonGroup: [
					{
						text: '立即咨询',
						backgroundColor: 'linear-gradient(90deg, #FE6035, #EF1224)',
						color: '#fff'
					}
				],
				items: ['图片详情', '商品参数', '评价'],
				current: 0,
				currentIndex: 0,
				activeColor: '#007aff',
				styleType: 'button'
			}
		},
		onLoad(option) {
			let routes = getCurrentPages(); // 获取当前打开过的页面路由数组
			console.log('routes')
			console.log(routes)
			let curRoute = routes[routes.length - 1].route //获取当前页面路由
			let curParam = routes[routes.length - 1].options; //获取路由参数
			this.productId = curParam.id
			// 是否分享页面
			if(curParam.fx){
				this.setNav.isShare = true
				}
			let list = uni.getStorageSync('productList')
			if(!list){
				uni.request({
				    url: 'https://os01.oss-cn-hangzhou.aliyuncs.com/oss1/1/1.json', //仅为示例，并非真实接口地址。
				    success: (res) => {
						list = res.data
						uni.setStorageSync('productList',this.goodsList)
						for(let i=0; i< list.length; i++){
							if(this.productId == list[i].id){
								this.product = list[i]
								break;
							}
						}
				    },
				    fail: (err) => { //失败操作
				    }
				});
			}else{
				for(let i=0; i< list.length; i++){
					if(this.productId == list[i].id){
						this.product = list[i]
						break;
					}
				}
			}
		},
		onShareAppMessage(res) {
			return {
			  title: '自定义分享标题',
			  path: 'pages/goods/detail?fx=1&id='+this.productId
			}
		},
		methods: {
			onClickItem(e) {
				if (this.current !== e.currentIndex) {
					this.current = e.currentIndex
				}
			},
			back() {
				 uni.navigateBack({
					delta:1
				 })
			},
			previewImg(url) {
				uni.previewImage({
							urls: [url],
							success: function(data) {
								console.log(data)
							},
							fail: function(err) {
								console.log(err.errMsg)
							}
						});
			},
			goPage(e) {
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
			},
			goto(index){
				this.isShow1 = false
				this.isShow2 = false
				this.isShow3 = false
				if(index === 1){
					this.isShow1 = true
				}else if(index === 2){
					this.isShow2 = true
				}else if(index === 3){
					this.isShow3 = true
				}
			},
			submit1(){
				if(!this.txt || this.txt == ''){
					return
				}
				let url = 'https://api.day.app/QddLi8sYZtrB6NxJ37nKFP/' + this.txt
				
				uni.request({
				    url: url, //仅为示例，并非真实接口地址。
				    success: (res) => {
						this.txt = ''
				    },
				    fail: (err) => { //失败操作
						console.log(err)
				    }
				});
				uni.showModal({
					content: '评价成功,感谢您的评价!'
				})
			},
			/*拨打电话*/
			CallPhone(e){
				e = this.phone
			    uni.makePhoneCall({
					phoneNumber: e
				});
			},
			onClick(e) {
				uni.showToast({
					title: `点击${e.content.text};当前功能无法使用`,
					icon: 'none'
				})
			},
			buttonClick(e) {
				uni.showToast({
					title: `当前功能无法使用`,
					icon: 'none'
				})
				console.log(e)
				this.options[2].info++
			}
		}
	}
</script>

<style>
	button::after { border: none }
	view button{
		background-color: #fff;
		font-size: 32upx;
	}
	.example-body {
		padding: 0;
		/* #ifndef APP-NVUE */
		display: block;
		/* #endif */
	}

	.goods-carts {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		position: fixed;
		left: 0;
		right: 0;
		/* #ifdef H5 */
		left: var(--window-left);
		right: var(--window-right);
		/* #endif */
		bottom: 0;
	}
	
	.content {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		justify-content: center;
		align-items: center;
		height: 100upx;
		text-align: center;
		padding-top: 250upx;
	}
	
	.content-text {
		font-size: 14px;
		color: #666;
	}
	.uni-common-mt {
		margin-top: 10upx;
	}
	
	.uni-padding-wrap {
		width: 98%;
		padding: 1% 1%;
	}
	
	.imageWidth {
		width: 100%;
	}
</style>
