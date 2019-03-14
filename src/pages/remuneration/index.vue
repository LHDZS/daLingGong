<style lang="less" scoped>
.remuneration {
    width: 100%;
    .title {
        width: 100%;
        height: 130rpx;
        .my_in {
            float: left;
            margin-top: 37rpx;
            margin-left: 30rpx;
            width:136rpx;
            height:56rpx;
            line-height: 56rpx;
            background:rgba(255,255,255,1);
            border:1rpx solid rgba(229,229,229,1);
            border-radius:28rpx;
            font-size:30rpx;
            font-family:PingFangSC-Regular;
            font-weight:400;
            color:rgba(51,51,51,1);
            position: relative;
            span {
                margin-left: 30rpx;
            }
            /*向下*/
            .triangle_border_down{
                position: absolute;
                top: 24rpx;
                right: 28rpx;
                width:0;
                height:0;
                border-width:12rpx 8rpx 0;
                border-style:solid;
                border-color:#999999 transparent transparent;/*灰 透明 透明 */
            }
        }
        .tit_text {
            float: right;
            margin-top: 28rpx;
            margin-right: 30rpx;
            text-align: center;
            font-size:26rpx;
            font-family:PingFangSC-Regular;
            font-weight:400;
            color:rgba(102,102,102,1);
        }
    }
    .main {
        width: 100%;
        background-color: #fff;
        .main_item {
            width: 100%;
            height: 142rpx;
            line-height: 142rpx;
            padding: 0 30rpx;
            // padding-top: 39rpx;
            box-sizing: border-box;
            border-bottom: 1rpx solid #e4e5ea;
            img {
                float: left;
                margin-top: 46rpx;
                margin-right: 30rpx;
                width: 54rpx;
                height: 54rpx;
            }
            .ma_item_text {
                float: left;
                margin-top: 30rpx;
                line-height: 35rpx;
                .tx1 {
                    font-size:30rpx;
                    font-family:PingFangSC-Regular;
                    font-weight:400;
                    color:rgba(51,51,51,1);
                    margin-bottom: 19rpx;
                }
                .tx2 {
                    font-size:26rpx;
                    font-family:PingFangSC-Regular;
                    font-weight:400;
                    color:rgba(153,153,153,1);
                }
            }
            .price {
                float: right;
                font-size:34rpx;
                font-family:PingFangSC-Regular;
                font-weight:400;
                color:rgba(231,92,68,1);
            }
        }
    }
    .timeSelector {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(255,255,255,0.5);
        padding-top: 140rpx;
        box-sizing: border-box;
        text-align: center;
    }
}
</style>

<template>
    <div class="remuneration">
        <div class="title">
            <div class="my_in" @click="month">
                <span>本月</span>
                <div class="triangle_border_down"></div>
            </div>
            <div class="tit_text">
                <div>本月收入：¥5000</div>
                <div style="margin-top:18rpx;">总收入：¥15000</div>
            </div>
        </div>
        <div class="main">
            <div class="main_item" v-for="(item,key) in remunerationArr" :key="key" @click="maindj(item)">
                <img src="/static/images/bcje.png" alt="">
                <div class="ma_item_text">
                    <div class="tx1">报酬-国美促销员</div>
                    <div class="tx2">今天 08:23</div>
                </div>
                <div class="price">+¥ 200</div>
            </div>
        </div>
        <div class="timeSelector" v-show="timeSelector">
            <picker-view
                indicator-style="height: 50px;"
                style="width: 100%; height: 300px;"
                :value="value"
                @change="bindChange"
                >
                <picker-view-column>
                <view v-for="(item,key) in years" :key="key" style="line-height: 50px">{{item}}年</view>
                </picker-view-column>
                <picker-view-column>
                <view v-for="(item,key) in months" :key="key" style="line-height: 50px">{{item}}月</view>
                </picker-view-column>
                <picker-view-column>
                <view v-for="(item,key) in days" :key="key" style="line-height: 50px">{{item}}日</view>
                </picker-view-column>
            </picker-view>
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            years:[],
            months:[],
            days:[],
            value:[9999, 1, 1],
            timeSelector:false,
            remunerationArr:[{},{},{},{},{}]
        }
    },
    onLoad() {
        wx.setNavigationBarTitle({
          title:'我的报酬',
        })
    },
    mounted () {
        const date = new Date()
        const years = []
        const months = []
        const days = []

        for (let i = 1990; i <= date.getFullYear(); i++) {
            this.years.push(i)
        }

        for (let i = 1; i <= 12; i++) {
            this.months.push(i)
        }

        for (let i = 1; i <= 31; i++) {
            this.days.push(i)
        }
    },
    methods: {
        month() {
            this.timeSelector = true
        },
        bindChange(e) {
            // const val = e.detail.value
            console.log(e.mp.detail.value)
        },
        maindj () {
            let url = '../billDetails/main'
            mpvue.navigateTo({ url })
        }
    }
}
</script>
