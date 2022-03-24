<template>

    <view class="page-body tui">
		<bar :nav="setNav"></bar>
        <nav class="uni-flex tui-bottom-nav" style="">

            <view class="uni-flex-item uni-flex tui-center" style="justify-content: space-around;padding: 0;font-size:1.5em;">
                <!-- <view class="tui-flex tui-column" style="line-height: 1.3em;" @tap="goPage('about')">
                    <text class="iconfont" style="font-size:1.5em;">&#xe8c7;</text>
                    <text style="font-size:0.6em ;">店家</text>
                </view> -->
                <!-- <view class="tui-flex tui-column" style="line-height: 1.3em;" @tap="goPage('chat')">
                    <text class="iconfont" style="font-size:1.5em;">&#xe8b4;</text>
                    <text style="font-size:0.6em ;">客服</text>
                </view>
                <view class="tui-flex tui-column" style="line-height: 1.3em;" @tap="goPage('chatIndex')">
                    <text class="iconfont" style="font-size:1.5em;">&#xe632;</text>
                    <text style="font-size:0.6em ;">消息</text>
                </view>
                <view class=" tui-flex tui-column" style="line-height: 1.3em;" @tap="goPage('wode')">
                    <text class="iconfont" style="font-size:1.5em;">&#xe604;</text>
                    <text style="font-size:0.6em ;">我的</text>
                </view>
                <view class=" tui-flex tui-column" style="line-height: 1.3em;padding: 0;" @tap="goPage('cart')">

                    <view class="iconfont" style="position: relative;" :style="cartItemCount?'color:red':''">
                        <view class="" style="font-size: 0.7em;position: absolute;right:30%;top:-10upx;right: 15px;">
                            <text style="font-size:0.5em ;" class="uni-badge uni-badge-danger">{{cartItemCount}}</text>
                        </view>
                        <text class="iconfont" style="font-size:1.5em;">&#xe8d2;</text>

                    </view>
                    <view style="font-size:0.6em;">¥{{cartTotal}}</view>
                </view> -->
                <!-- 导航微信 -->
            </view>
        </nav>

        <view v-if="isShow" class="main-content tui-flex tui-row" :style="{height:contentHeight + 'px'}">

            <scroll-view scroll-y class="tui-flex tui-center tui-column" style="width: 180upx; " :style="{height:contentHeight + 'px'}">
                <view class="tui-item tui-border cebian-list" @click="categoryClickMain(null,{id:null})" :class="categoryActive==null?'active':''">
                    全部
                </view>

                <view class="tui-item cebian-list tui-border tui-relative" @click="categoryClickMain(idx,item)" :key="idx"
                    :style="idx==categoryActive?'opacity:0.7;color:red':'opacity:1;color:;'" v-for="(item,idx) in category">
                    {{item.name}}
                    <view class="tui-nav-badge tui-absolute" style="top:0;right: 0;">
                        <text v-if="item.total" class="uni-badge uni-badge-warning">{{item.total}}</text>
                    </view>
                </view>
            </scroll-view>
            <scroll-view class="uni-flex-item" scroll-y :style="{height:contentHeight + 'px'}" style="width: 570upx;">
                <!-- <view class="content-right" v-if="goodsList"> -->
                <view v-if="categoryId==item.category_id||categoryId==null" class="tui-flex tui-border tui-list" style=""
                    v-for="(item,key) in goodsList" :key="key">
                    <view class="">
                        <image style="height:130upx;width: 130upx;" :src="item.image" mode="aspectFill" />
                    </view>
                    <!-- @tap="tapDetail(item,key,item.selected);" -->

                    <view class="tui-flex tui-column" style="box-sizing: border-box;padding-left:100upx;height: 135upx;width: 400upx;">
                        <view class="tui-title">{{item.title}}</view>
                        <view style="display: flex;justify-content: space-between;">
                            <view class="">
                                <text style="color: red;">{{item.price}} 元</text>
                            </view>
                            <!-- <view class="tui-center" style="display: flex;">
                                <text class="iconfont" :class="cart[item.id] && cart[item.id].number && cart[item.id].number>0 ?'color-ju':''"
                                    @tap="selectList(item,key,'-')" style="width: 50upx;font-size: 1.3em;">&#xe756;</text>
                                <view class="" style="width: 50upx;">
                                    <text v-if=" cart[item.id]">{{cart[item.id].number}}</text>
                                    <text v-else>0</text>
                                </view>
                                <text class="iconfont" :class="cart[item.id] && cart[item.id].number && cart[item.id].number<cart[item.id].stock ?'color-ju':''"
                                    style="width: 50upx;font-size: 1.3em;" @tap="selectList(item,key,'+')">&#xe600;</text>
                            </view> -->
                        </view>
                       <!-- <view v-if="item.version[0]" class="" style="white-space:nowrap;overflow-y:hidden;width:350upx;">
                            <text class="uni-badge" @tap="versionTap(item,vIdx)" v-for="(vn,vIdx) in item.version" :key="vIdx"
                                style="max-width: 100%;font-size: 0.8em;" :style="item.versionName==vn.name?'color:red':''">{{vn.name}}</text>

                        </view> -->

                    </view>

                </view>
                <!-- </view> -->
            </scroll-view>
        </view>

    </view>
</template>

<script>
	import bar from "@/components/template/nav/bar.vue"
    // import numberBox from '../../components/template/box/number.vue'
    import {Storage} from '@/common/yc_js/';
    // import uniDrawer from '../../components/template/drawer/drawer.vue';
    import Request from "../../request/index.js"
    var timeOut = '';
    export default {
        components: {
			bar
            // uniDrawer,
            // uniIcon,
        },
        data() {
            return {

                winHeight: 0,
                contentHeight: 0,
                categoryActive: 0,
                categoryId: null,
                index: 0,
                isShow: true,
				setNav:{
					'bg':'',  //背景色
					'color':'white',  //字体颜色
					'isdisPlayNavTitle':false, //是否显示返回按钮，由于导航栏是共用的，把所有的东西封装好，
					// 然后有些页面不需要的东西通过条件控制进行显示与隐藏
					'navTitle':'商品列表' //导航标题
				},
                goods: {
                    id: 1,
                    image: 'https://img-cdn-qiniu.dcloud.net.cn/uploads/example/product3.jpg',
                    title: '新鲜梨花带雨',
                    price: 0.01,
                    stock: 12,
                    number: 0,
                    versionName: '未选择',
                    versionIdx: '',
                    synopsis: "简介，这里是梨花带雨详情",
                    version: [{
                        name: '大份',
                        price: 18,
                        stock: 6,
                        image: ''
                    }]
                },
                goodsList: [
					// {
					// 	id: 1,
					// 	image: 'https://os01.oss-cn-hangzhou.aliyuncs.com/oss1/1/1.jpg',
					// 	title: '青蛙牌单相井用水泵',
					// 	price: 1320,
					// 	stock: 12,
					// 	category_id: 1,
					// 	number: 1
					// },
					// {
					// 	id: 2,
					// 	image: 'https://os01.oss-cn-hangzhou.aliyuncs.com/oss1/1/3.jpg',
					// 	title: '揉草机',
					// 	price: 1750,
					// 	stock: 12,
					// 	category_id: 1,
					// 	number: 1
					// },
					// {
					// 	id: 3,
					// 	image: 'https://os01.oss-cn-hangzhou.aliyuncs.com/oss1/1/4.jpg',
					// 	title: '加面机',
					// 	price: 1050,
					// 	stock: 12,
					// 	category_id: 1,
					// 	number: 1
					// },
					// {
					// 	id: 4,
					// 	image: 'https://os01.oss-cn-hangzhou.aliyuncs.com/oss1/1/5.jpg',
					// 	title: '打玉米5',
					// 	price: 580,
					// 	stock: 12,
					// 	category_id: 1,
					// 	number: 1
					// },
					// {
					// 	id: 5,
					// 	image: 'https://os01.oss-cn-hangzhou.aliyuncs.com/oss1/1/6.jpg',
					// 	title: '侧草带加面机器',
					// 	price: 1500,
					// 	stock: 12,
					// 	category_id: 1,
					// 	number: 1
					// }
				], //商品列表\
                totalCart: 0, //购物车商品总数量
                category: [
					 {
                        name: '农机具',
                        id: '1',
                    },
                    {
                        name: '工具包',
                        id: '2',
                    },
                    {
                        name: '插排',
                        id: '3'
                    },
                    {
                        name: '水管',
                        id: '4'
                    },
                    // {
                    //     name: '粗茶',
                    //     id: '5',
                    // }
                ],
            };
        },
        computed: {
            cartItemCount: {
                get() {
                    // console.log(this.$store.getters.cartItemCount)
                    return this.$store.getters.cartItemCount
                }
            },
            cartTotal: {
                get() {
                    return this.$store.getters.cartTotal
                }

            },
            cart: {
                get() {
                    return this.$store.getters.cart
                }
            },
            Cartlist: {
                set(value) {
                    this.shopCart = value;
                },
                get() {
                    return this.shopCart;
                }
            }
        },
        mounted: function() {

            let winHeight = uni.getSystemInfoSync().windowHeight;
            //创建节点选择器 获取底部导航高度 
            this.contentHeight = (winHeight - uni.upx2px(100));
            this.winHeight = winHeight;
            // this.$store.commit('shop',{shop_id:1,shop_name:"新店铺"})


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
        onLoad(e) {
            this.$store.commit('init')
			uni.showModal({
				content: '只介绍有哪些产品、标价。如有需求可电话联系购买                                         手机号：150 4769 0961'
			})
            var id = e.id || '1';
            console.log(e)
            // 请求服务器
            var self = this;
			// setTimeout(function () {
			// }, 3000);

            // var host=this.$config.host+"shop/"+id;//主服务器地址

            // Request("goodsShop", {
            //     data: {
            //         id: id
            //     }
            // }).then((res) => {
            //     var data = res.data.data
            //     var goodsList = data.goodsList;
            //     var shop = {}
            //     shop.shop_id = data.shop_id;
            //     shop.shop_name = data.shop_name;
            //     self.$store.commit('shop', shop)
            //     console.log(self.$store.getters.shop)
            //     console.log(res.data.data)
            //     // var shops=res.data.data ||{};
            //     for (let i = 0; i < goodsList.length; i++) {
            //         // 判断图片地址是站内或站外，替换链接地址http
            //         let src = '';
            //         if (goodsList[i].image.indexOf("http") < 0) {
            //             src = this.$config.server.image;
            //         }
            //         goodsList[i].image = src + goodsList[i].image;
            //     }
            //     self.goodsList = goodsList;
            //     var category = res.data.data.category;

            //     uni.hideLoading();
            //     self.category = category;
            // })
			uni.request({
			    url: 'https://os01.oss-cn-hangzhou.aliyuncs.com/oss1/1/1.json', //仅为示例，并非真实接口地址。
			    success: (res) => {
					this.goodsList = res.data
			    },
                fail: (err) => { //失败操作
                }
			});
        },
        methods: {
            versionTap(item, index) {
                item.selected = true;
                this.$store.commit('version', {
                    goods: item,
                    index: index
                })
                // 				uni.showModal({
                // 					title:"提示",
                // 					content:"请在下单后进行选择"
                // 				})		
            },
            goodsUpdate(e) {
                // console.log(e)
                console.log('goodsUpdate')
                this.$set(this.goodsList[this.detailIndex], this.detailIndex, e)
                // this.categoryList[this.detailIndex]=e;
                this.selectList(this.detailIndex)
            },
            // 			commit(){
            // 				
            // 				this.$set(this.goodsList,this.detailIndex,this.detail)
            // 			},

            goPage(e) {
                var url = '';
                switch (e) {
                    case "cart":
                        var goods = this.goodsList;
                        var cart = {};
                        // cart[this.goods.id]=this.goods;
                        for (let i = 0; i < goods.length; i++) {
                            if (goods[i].selected) {
                                cart[goods[i].id] = goods[i];
                            }
                        }
                        Storage.set('cart', cart, 1000);
                        url = "/pages/goods/" + e + "?id=2";
                        break;
                    case "wode":
                        url = "/pages/user/" + e + "?id=2";
                        break;
                    case "chat":
                        url = "/pages/chat/" + e + "?id=2";
                        break;
                    case "order":
                        url = "/pages/order/list?id=2";
                        break;
                    case "chatIndex":
                        url = "/pages/chat/index";
                        break;
                    default:
                        url = "/pages/goods/" + e + "?id=2";
                        break;
                }


                uni.navigateTo({
                    url: url,
                    success: res => {

                    },
                    fail: () => {},
                    complete: () => {}
                });
            },
            // 			countSelect(){
            // 				
            // 			},
            // 购物车增减商品
            selectList(item, index, selected) {
                item.selected = true;

                this.$store.commit('addCart', {
                    goods: item,
                    methods: selected
                })
                this.$set(this.goodsList, index, this.goodsList[index])

            },

            categoryClickMain(idx, item) {
                this.categoryId = item.id;
                this.categoryActive = idx;
            },

        }
    }
</script>

<style>
    .tui-box::-webkit-scrollbar {
        display: none;
    }

    .scrollList {
        flex: 1;
        height: 100vh;
    }

    .cebian-list {
        width: 180upx;
        font-size: 1em;
        line-height: 3em;
    }

    .content-right {
        text-align: left;
    }

    /* 侧边菜单 */
    .header {
        display: flex;
        flex-direction: row;
        padding: 10px 15px;
        align-items: center;
    }

    .input-view {
        display: flex;
        align-items: center;
        flex-direction: row;
        background-color: #e7e7e7;
        height: 30px;
        border-radius: 15px;
        padding: 0 10px;
        flex: 1;
    }

    .input {
        flex: 1;
        padding: 0 5px;
        height: 24px;
        line-height: 24px;
        font-size: 16px;
    }

    .icon {
        display: flex;
        flex-direction: column;
        justify-content: center;
        margin-left: 10px;
    }


    .drawer-content {
        padding: 15px;
    }

    .drawer-content>.title {
        font-size: 18px;
    }

    .drawer-content>.text {
        font-size: 15px;
    }

    .drawer-content>.button {
        font-size: 14px;
    }

    /* 侧边菜单完*/
</style>
