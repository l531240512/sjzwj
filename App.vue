<script>
	import Vue from 'vue'
    export default {
        computed: {
            // this.$store.getters.user;    
        },
        mounted() {
            var that = this;
            // 监听窗口宽高变化
            (function screenListener() {
                uni.onWindowResize((res) => {
                    that.$store.commit('screen', {
                        width: res.size.windowWidth,
                        height: res.size.windowHeight
                    });
                    // 					console.log('变化后的窗口宽度=' + res.size.windowWidth)
                    // 					console.log('变化后的窗口高度=' + res.size.windowHeight)
                })
            })()
        },
        onLaunch: function() {
           uni.getSystemInfo({
             success:function(e){
              Vue.prototype.statusBar = e.statusBarHeight
              // #ifndef MP
              if(e.platform == 'android') {
               Vue.prototype.customBar = e.statusBarHeight + 50
              }else {
               Vue.prototype.customBar = e.statusBarHeight + 45
              }
              // #endif
              
              // #ifdef MP-WEIXIN
              let custom = wx.getMenuButtonBoundingClientRect()
              Vue.prototype.customBar = custom.bottom + custom.top - e.statusBarHeight
              // #endif
              
              // #ifdef MP-ALIPAY
              Vue.prototype.customBar = e.statusBarHeight + e.titleBarHeight
              // #endif
             }
            }) 
        },
        onShow: function() {
            console.log('App Show')
        },
        onHide: function() {
            console.log('App Hide')
        }
    }
</script>

<style>
    /* uni.css - 通用组件、模板样式库，可以当作一套ui库应用 */
    @import "./common/uni.css";
    /* @import "./common/css/iconfont.css"; */
    @import "./common/css/tui.css";
    @import "./common/yc.css";

    .color-font {
        color: #F7F7F7;
    }

    .color-background {
        color: #333333;
        background: #F7F7F7;
    }
    .color-nav{
        background: #0A98D5;
        color: #ffffff;
    }
    /* 以下样式用于 hello uni-app 演示所需 */
    page {
        color: #666;
        background-color: #F4F5F6;
        height: 100%;
        font-size: 28upx;
        /* overflow: hidden; *//* 注释解开会导致也没无法上下滚动 */
    }

    .page-body {
        padding: 0;
        margin: 0;
        justify-content: space-between;
        flex-direction: column;
        align-content: ;
        height: 100vh;
        box-sizing: border-box;
        display: flex;
    }

    /* 	.main-content{
		margin-bottom: 100upx;
		text-align: center;
		width: 100%;
		flex:1;
		overflow-y:auto;
		box-sizing:border-box;
	} */
    .uni-input-group .uni-input-row:after {
        right: 10upx;
        left: 10upx;
    }

    .uni-input-row input {
        flex: 1;
        padding: 0 10upx;
        border-radius: 6upx;
        background: #E9E9E9;
    }

    .uni-input-row .uni-label {
        text-indent: 0;
        flex-direction: column;
        display: flex;
        justify-content: center;
        text-align: center;
    }
</style>
