<style lang="less" scoped>
.myNews {
    width: 100%;
    height: 100%;
    background-color: #fff;
    .title {
        width: 100%;
        padding: 20rpx;
        box-sizing: border-box;
        border-bottom:1rpx solid #e4e5ea;
        overflow: hidden;
        .button {
            float: right;
            width:131rpx;
            height:48rpx;
            border:1px solid rgba(9,165,254,1);
            border-radius:24rpx;
            line-height: 48rpx;
            text-align: center;
            color: #09A5FE;
            font-size: 24rpx;
        }
    }
    .myNews_item {
        width: 100%;
        height: 104rpx;
        padding-top: 10rpx;
        box-sizing: border-box;
        .myNews_img {
            float: left;
            width: 70rpx;
            height: 70rpx;
            background: rgba(255,255,255,1);
            border: 1rpx solid rgba(229,229,229,1);
            border-radius: 6rpx;
            padding: 14rpx;
            box-sizing: border-box;
            img {
                width: 40rpx;
                height: 40rpx;
            }
        }
        .item_right {
            float: right;
            width: calc(100% - 85rpx);
            height: 100%;
            font-family:PingFangSC-Regular;
            font-weight:400;
            .top {
                width: 100%;
                height: 60%;
                .left {
                    float: left;
                    font-size:30rpx;
                    color:rgba(51,51,51,1);
                }
                .right {
                    float: right;
                    font-size:24rpx;
                    color:rgba(204,204,204,1);
                }
            }
            .bottom {
                width: 100%;
                height: 40%;
                font-size:26rpx;
                color:rgba(153,153,153,1);
            }
        }
        
    }
    .noMessage {
        width: 100%;
        margin-top: 223rpx;
        text-align: center;
        img {
            width: 111rpx;
            height: 133rpx;
        }
        div {
            width: 100%;
            padding-left: 5rpx;
            margin-top: 49rpx;
            font-size:30rpx;
            font-family:PingFangSC-Regular;
            font-weight:400;
            color:rgba(136,136,136,1);
        }
    }
}
</style>

<template>
    <div class="myNews">
        <div class="The_divider"></div>
        <div class="title">
            <div class="button">
                全部已读
            </div>
        </div>
        <div v-if="myNewsArr.lenght != 0">
            <i-swipeout  i-class="i-swipeout-demo-item" :operateWidth="87" :actions="actions" @change="dj">
                <div class="myNews_item" slot="content">
                    <i-badge dot>
                        <div class="myNews_img">
                            <img src="/static/images/dzt.png" alt="">
                        </div>
                    </i-badge>
                    <div class="item_right">
                        <div class="top">
                            <div class="left">到账成功</div>
                            <div class="right">2019-02-20 10:00:34</div>
                        </div>
                        <div class="bottom">您的订单【国美 促销员】120元／天薪酬...</div>
                    </div>
                </div>
            </i-swipeout>
            <i-swipeout  i-class="i-swipeout-demo-item" :operateWidth="87" :actions="actions" @change="dj">
                <div class="myNews_item" slot="content">
                    <i-badge dot>
                        <div class="myNews_img">
                            <img src="/static/images/sht.png" alt="">
                        </div>
                    </i-badge>
                    <div class="item_right">
                        <div class="top">
                            <div class="left">到账成功</div>
                            <div class="right">2019-02-20 10:00:34</div>
                        </div>
                        <div class="bottom">您的订单【国美 促销员】120元／天薪酬...</div>
                    </div>
                </div>
            </i-swipeout>
            <i-swipeout  i-class="i-swipeout-demo-item" :operateWidth="87" :actions="actions" @change="dj">
                <div class="myNews_item" slot="content">
                    <i-badge dot>
                        <div class="myNews_img">
                            <img src="/static/images/rzt.png" alt="">
                        </div>
                    </i-badge>
                    <div class="item_right">
                        <div class="top">
                            <div class="left">到账成功</div>
                            <div class="right">2019-02-20 10:00:34</div>
                        </div>
                        <div class="bottom">您的订单【国美 促销员】120元／天薪酬...</div>
                    </div>
                </div>
            </i-swipeout>
            <i-swipeout  i-class="i-swipeout-demo-item" :operateWidth="87" :actions="actions" @change="dj">
                <div class="myNews_item" slot="content">
                    <i-badge dot>
                        <div class="myNews_img">
                            <img src="/static/images/xtt.png" alt="">
                        </div>
                    </i-badge>
                    <div class="item_right">
                        <div class="top">
                            <div class="left">到账成功</div>
                            <div class="right">2019-02-20 10:00:34</div>
                        </div>
                        <div class="bottom">您的订单【国美 促销员】120元／天薪酬...</div>
                    </div>
                </div>
            </i-swipeout>
        </div>
        
        <div class="noMessage" v-if="myNewsArr.lenght == 0">
            <img src="/static/images/zwxx.png" alt="">
            <div>暂无信息</div>
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            num:1,
            myNewsArr:[{},{},{},{}],
            actions : [
                {
                    name : '删除',
                    color : '#fff',
                    fontsize : '20',
                    width : 100,
                    icon : 'trash',
                    background : '#2d8cf0'
                }
            ]
        }
    },
    onLoad() {
        wx.setNavigationBarTitle({
          title:'我的消息(' + this.num + ')',
        })
    },
    mounted () {
        
    },
    methods: {
        dj(i) {
            console.log(i)
        }
    }
}
</script>
