<style lang="less" scoped>
.found {
    width: 100%;
    height: 100%;
    background-color: #fff;
    padding-top: 21rpx;
    box-sizing: border-box;
    .found_swipe {
        width: 690rpx;
        height: 235rpx;
        margin: 0 auto;
        border-radius:12rpx;
        overflow: hidden;
    }
    .f_title {
        width: 100%;
        text-align: center;
        font-size:36rpx;
        font-family:PingFangSC-Regular;
        font-weight:400;
        color:rgba(51,51,51,1);
        line-height:48rpx;
        margin-top: 50rpx;
    }
    .main {
        width: 100%;
        padding: 35rpx;
        box-sizing: border-box;
        .main_list {
            float: left;
            width: 195rpx;
            height: 195rpx;
            border:1rpx solid rgba(216,216,216,1);
            border-radius:6rpx;
            margin: 15rpx;
            font-size:32rpx;
            font-family:PingFangSC-Regular;
            font-weight:400;
            color:rgba(51,51,51,1);
            text-align: center;
            img {
                margin-top: 36rpx;
                width: 68rpx;
                height: 68rpx;
            }
        }
    }
    .maskLayer {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0,0,0,0.8);
        .content {
            margin: 0 auto;
            margin-top: 342rpx;
            width:527rpx;
            height:450rpx;
            background:rgba(255,255,255,1);
            border-radius:16rpx;
            padding: 48rpx;
            box-sizing: border-box;
            font-size:28rpx;
            font-family:PingFangSC-Regular;
            font-weight:400;
            color:rgba(102,102,102,1);
            line-height: 48rpx;
            .title {
                width: 100%;
                text-align: center;
                font-size:36rpx;
                font-family:PingFangSC-Regular;
                font-weight:400;
                color:rgba(9,165,254,1);
                line-height:61rpx;
                margin-bottom: 34rpx;
            }
            .button {
                margin: 0 auto;
                margin-top: 40rpx;
                width:410rpx;
                height:76rpx;
                text-align: center;
                line-height: 76rpx;
                background:rgba(9,165,254,1);
                border-radius:38rpx;
                font-size:28rpx;
                font-family:SourceHanSansCN-Regular;
                font-weight:400;
                color:rgba(255,255,255,1);
            }
        }
    }
}
</style>

<template>
    <div class="found">
        <div class="found_swipe">
            <swiper
                :indicator-dots="indicatorDots"
                :autoplay="autoplay"
                :interval="interval"
                :duration="duration"
                indicator-color="rgba(255, 255, 255, 0.5)"
                indicator-active-color="rgba(255, 255, 255, 1)"
                style="height: 235rpx;"
                >
                <block v-for="(item,key) in imgUrls" :key="key">
                <swiper-item>
                    <img :src="item" class="found_image"/>
                </swiper-item>
                </block>
            </swiper>
        </div>
        <div class="f_title">- 第三方服务 -</div>
        <div class="main clearfix">
            <div class="main_list" v-for="(list,key) in foundArr" :key="key" @click="find">
                <img :src="list.img" alt="">
                <div>{{list.name}}</div>
            </div>
        </div>
        <div class="maskLayer" v-if="maskLayerType">
            <div class="content">
                <div class="title">- 免责声明 -</div>
                <div>
                    本服务由中关村银行提供。 相关服务和责任将由该第三方承担。 如有问题请咨询该公司客服。
                </div>
                <div class="button" @click="knowThe">知道了</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            // swiper
            imgUrls: [
                '/static/images/swipe-img.png',
                '/static/images/swipe-img.png',
                '/static/images/swipe-img.png'
            ],
            indicatorDots: true,
            autoplay: true,
            interval: 5000,
            duration: 1000,
            // 九宫格
            foundArr:[
                {
                    img:'/static/images/lc.png',
                    name:'理财'
                },{
                    img:'/static/images/jq.png',
                    name:'借钱'
                },{
                    img:'/static/images/bx.png',
                    name:'保险'
                },{
                    img:'/static/images/xyk.png',
                    name:'信用卡'
                },{
                    img:'/static/images/zfdk.png',
                    name:'租房贷款'
                },{
                    img:'/static/images/cd.png',
                    name:'车贷'
                },{
                    img:'/static/images/jsb.png',
                    name:'缴社保'
                },{
                    img:'/static/images/jgjj.png',
                    name:'缴公积金'
                }
            ],
            maskLayerType:false,
        }
    },
    methods: {
        find () {
            this.maskLayerType = true
        },
        knowThe() {
            this.maskLayerType = false
        }
    }
}
</script>
