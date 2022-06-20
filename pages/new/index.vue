<template>
	<view class="warp">
		<bar :nav="setNav"></bar>
		<view style="height: 100upx;">
			<view style="margin-left: 50upx; margin-top: 50upx; font-size:32upx; font-weight:bold; letter-spacing:2upx;">
				<text class="flex flex-direction">内蒙古赤峰市敖汉旗四家子镇</text>
			</view>
			<view style="margin-left: 50upx; margin-top: 20upx; color:darkgrey">
				<text class="flex flex-direction">时间：2022-1-1</text>
			</view>
		</view>
		<view class="uni-padding-wrap uni-common-mt">
			<view>
				<video id="myVideo" src="https://img.cdn.aliyun.dcloud.net.cn/guide/uniapp/%E7%AC%AC1%E8%AE%B2%EF%BC%88uni-app%E4%BA%A7%E5%93%81%E4%BB%8B%E7%BB%8D%EF%BC%89-%20DCloud%E5%AE%98%E6%96%B9%E8%A7%86%E9%A2%91%E6%95%99%E7%A8%8B@20200317.mp4"
					@error="videoErrorCallback" :danmu-list="danmuList" enable-danmu danmu-btn controls></video>
			</view>
			<!-- #ifndef MP-ALIPAY -->
			<view class="uni-list uni-common-mt">
				<view class="uni-list-cell">
					<view>
						<view class="uni-label">弹幕内容</view>
					</view>
					<view class="uni-list-cell-db">
						<input v-model="danmuValue" class="uni-input" type="text" @confirm="sendDanmu" placeholder="在此处输入弹幕内容" />
					</view>
				</view>
			</view>
			<!-- #endif -->
		</view>
		<view style="margin-left: 50upx; margin-right: 50upx;margin-top: 50upx;">
			<view>
				<p style="text-indent: 60upx;"> 四家子镇，隶属于内蒙古赤峰市敖汉旗，地处敖汉旗南部，东南、南与辽宁省朝阳市朝阳县毗邻，西南、西、西北与辽宁省朝阳市建平县相连，北与新惠镇为邻，东北与金厂沟梁镇接壤。  四家子镇行政区域面积425.74平方千米。2018年末，四家子镇户籍人口45042人。 </p> 
			</view>
			<view style="margin-top: 50upx;">
				<h1>历史沿革</h1> 
				<ol>
					<li>
						清光绪二十九年（1903年），属敖汉札萨克多罗郡王旗四家子乡四家子牌。
					</li>
					<li>
						宣统三年（1911年），属敖汉左翼札萨克多罗郡王旗。
					</li>
					<li>
						1956年9月，境内建四家子、小古力吐、牛夕何屯3乡，均属敖汉旗四家子区。
					</li>
					<li>
						1958年10月，成立四家子公社。
					</li>
					<li>
						1966年9月，改称四新公社。
					</li>
					<li>
						1972年12月，复称四家子公社。
					</li>
					<li>
						1984年2月，改四家子镇，人民政府驻地四家子村。
					</li>
					<li>
						2006年1月，林家地乡并入。
					</li>
					
				</ol>
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
				title: '地址：敖汉旗四家子镇四家子村邮局斜对面',
				// 自定义导航栏对象
				setNav:{
					'bg':'linear-gradient(to right, #FFFFFF, #FFFFFF)',  //背景色
					'color':'white',  //字体颜色
					'isdisPlayNavTitle':true, //是否显示返回按钮，由于导航栏是共用的，把所有的东西封装好，
					// 然后有些页面不需要的东西通过条件控制进行显示与隐藏
					'navTitle':'五金' //导航标题
				},
				src: '',
				danmuList: [{
						text: '第 1s 出现的弹幕',
						color: '#ff0000',
						time: 1
					},
					{
						text: '第 3s 出现的弹幕',
						color: '#ff00ff',
						time: 3
					}
				],
				danmuValue: ''
			}
		},
		onLoad() {

		},
		onShareAppMessage() {
			return {
			  title: '自定义分享标题',
			  path: 'pages/new/index'
			}
		},
		onReady: function(res) {
		    // #ifndef MP-ALIPAY
		    this.videoContext = uni.createVideoContext('myVideo')
		    // #endif
		},
		methods: {
			sendDanmu: function() {
			    this.videoContext.sendDanmu({
			        text: this.danmuValue,
			        color: this.getRandomColor()
			    });
			    this.danmuValue = '';
			},
			videoErrorCallback: function(e) {
			    uni.showModal({
			        content: e.target.errMsg,
			        showCancel: false
			    })
			},
			getRandomColor: function() {
			    const rgb = []
			    for (let i = 0; i < 3; ++i) {
			        let color = Math.floor(Math.random() * 256).toString(16)
			        color = color.length == 1 ? '0' + color : color
			        rgb.push(color)
			    }
			    return '#' + rgb.join('')
			},
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
			back() {
				 uni.navigateBack({
					delta:1
				 })
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
				// uni.navigateTo({
				//     url: url,
				//     success: res => {
				// 		console.log(res);
				//     },
				//     fail: (res) => {
				// 		console.log(res);
				// 	},
				//     complete: () => {}
				// });
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
	
	view ol li {
		font-size: 21upx; 
		margin-top: 15upx; 
		/* text-indent: 60upx; */
	}
	
	view video {
		width: 100%;
	}
</style>
