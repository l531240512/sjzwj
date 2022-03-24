<template>
	<view class="warp">
		<bar :nav="setNav"></bar>
		<view style="height: 200upx;">
			<view style="margin-left: 50upx; margin-top: 50upx; font-size:32upx; font-weight:bold; letter-spacing:2upx;">
				<text class="flex flex-direction">内蒙古赤峰市敖汉旗四家子镇</text>
			</view>
			<view style="margin-left: 50upx; margin-top: 20upx; color:darkgrey">
				<text class="flex flex-direction">时间：2022-1-1</text>
			</view>
		</view>
		<view style="margin-left: 50upx; margin-right: 50upx;">
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
				}
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
</style>
