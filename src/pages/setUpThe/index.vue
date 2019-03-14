<style lang="less" scoped>
.setUpThe {
    width: 100%;
    .sut_phone {
        width: 100%;
        height: 111rpx;
        line-height: 111rpx;
        font-size:30rpx;
        font-family:PingFangSC-Regular;
        font-weight:400;
        color:rgba(51,51,51,1);
        padding-left: 39rpx;
        box-sizing: border-box;
        background-color: #fff;
        border-top: 1rpx solid #e4e5ea;
        color:rgba(102,102,102,1);
        .Modify_the {
            float: left;
        }
        .call {
            width:108rpx;
            height:48rpx;
            margin-top: 30rpx;
            line-height: 48rpx;
            text-align: center;
            font-size:26rpx;
            font-family:PingFangSC-Regular;
            font-weight:400;
            color:rgba(9,165,254,1);
            border:1px solid rgba(9,165,254,1);
            border-radius:6px;
            float: right;
            margin-right: 23rpx;
        }
        span {
            margin-right: 58rpx;
        }
    }
    .exit {
        position: fixed;
        left: 92rpx;
        bottom: 70rpx;
        width: 566rpx;
        height: 84rpx;
        line-height: 84rpx;
        text-align: center;
        border:1px solid rgba(216,216,216,1);
        border-radius:42px;
        font-size:38rpx;
        font-family:SourceHanSansCN-Regular;
        font-weight:400;
        color:rgba(102,102,102,1);
    }
}
</style>

<style lang="less">
page {
    background-color: #fff;
}
</style>


<template>
    <div class="setUpThe">
        <div class="sut_phone" @click="detailspage">
            <div class="Modify_the">修改绑定手机</div>
            <i-icon type="enter" style="float:right;margin-right:41rpx" />
        </div>
        <div class="sut_phone">
            <span>客服电话</span>
            <span>4006-798-999</span>
            <div class="call" @click="upthe">拨打</div>
        </div>
        <div class="The_divider"></div>
        <div class="exit">退出登录</div>
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
          title:'设置',
        })
    },
    mounted () {
        
    },
    methods: {
        detailspage () {
            let url = '../modifyPhone/main'
            mpvue.navigateTo({ url })
        },
        upthe() {
            mpvue.makePhoneCall({
                phoneNumber: '4006-798-999'
            })
        }
    }
}
</script>
