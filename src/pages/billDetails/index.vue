<style lang="less" scoped>
.billDetails {
    width: 100%;
    .title {
        width: 100%;
        height: 265rpx;
        font-family:PingFangSC-Regular;
        font-weight:400;
        text-align: center;
        border-top: 1rpx solid #e4e5ea;
        border-bottom: 1rpx solid #e4e5ea;
        .price {
            width: 100%;
            margin-top: 38rpx;
            font-size:55rpx;
            color:rgba(231,92,68,1);
        }
        .text {
            width: 100%;
            font-size:26rpx;
            color:rgba(153,153,153,1);
        }
        .describe {
            width: 100%;
            margin-top: 30rpx;
            font-size:34rpx;
            color:rgba(34,34,34,1);
            img {
                width: 46rpx;
                height: 46rpx;
                margin-top: -10rpx;
                margin-right: 20rpx;
                vertical-align: middle;
            }
        }
    }
    .main {
        width: 100%;
        .main_list {
            width: 100%;
            height: 88rpx;
            line-height: 88rpx;
            font-family:PingFangSC-Regular;
            font-weight:400;
            font-size:30rpx;
            padding: 0 30rpx;
            box-sizing: border-box;
            .listext1 {
                float: left;
                color:rgba(153,153,153,1);
            }
            .listext2 {
                float: right;
                color:rgba(51,51,51,1);
            }
        }
    }
}
</style>

<style lang="less">
page {
    background-color: #fff;
}
</style>


<template>
    <div class="billDetails">
        <div class="title">
            <div class="price">+200</div>
            <div class="text">交易成功</div>
            <div class="describe">
                <img src="/static/images/bcje.png" alt="">
                <span>国美电器有限公司</span>
            </div>
        </div>
        <div class="main">
            <div class="main_list">
                <div class="listext1">账单说明</div>
                <div class="listext2">促销员报酬发放</div>
            </div>
        </div>
        <div class="main">
            <div class="main_list">
                <div class="listext1">对方账户</div>
                <div class="listext2">国美电器有限公司</div>
            </div>
        </div>
        <div class="main">
            <div class="main_list">
                <div class="listext1">创建时间</div>
                <div class="listext2">2019-02-21 08:00:23</div>
            </div>
        </div>
        <div class="main">
            <div class="main_list">
                <div class="listext1">订单编号</div>
                <div class="listext2">29988932940300000000</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            
        }
    },
    onLoad() {
        wx.setNavigationBarTitle({
          title:'账单详情',
        })
    },
    mounted () {
        
    },
    methods: {
        
    }
}
</script>
