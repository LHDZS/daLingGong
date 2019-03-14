<style lang="less" scoped>
.certificationPrompt {
    width: 100%;
    height: 100%;
    background-color: #fff;
    padding-top: 120rpx;
    box-sizing: border-box;
    .cfp_img {
        width: 213rpx;
        height: 128rpx;
        margin: 0 auto;
    }
    .cfp_text {
        width: 100%;
        padding-left: 5rpx;
        margin-top: 41rpx;
        text-align: center;
        font-size:40rpx;
        font-family:PingFangSC-Regular;
        font-weight:400;
        color:rgba(51,51,51,1);
    }
    .cfp_imgoff {
        width: 118rpx;
        height: 118rpx;
        margin: 0 auto;
    }
    .cfp_button {
        margin: 0 auto;
        margin-top: 30rpx;
        width:236rpx;
        height:70rpx;
        line-height: 70rpx;
        text-align: center;
        border:2rpx solid rgba(9,165,254,1);
        border-radius:35rpx;
        font-size:30rpx;
        font-family:PingFangSC-Regular;
        font-weight:400;
        color:rgba(9,165,254,1);
    }
}
</style>

<template>
    <div class="certificationPrompt">
        <div class="cfp_img" v-if="imgOffOn">
            <img src="/static/images/rzcg.png" alt="">
        </div>
        <div class="cfp_text" v-if="imgOffOn">认证成功!</div>
        <div class="cfp_imgoff" v-if="!imgOffOn">
            <img src="/static/images/rzsb.png" alt="">
        </div>
        <div class="cfp_text" v-if="!imgOffOn">认证失败</div>
        <div class="cfp_button" v-if="!imgOffOn" @click="recertification">重新认证</div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            imgOffOn:false
        }
    },
    onLoad(options) {
        wx.setNavigationBarTitle({
          title:'身份认证',
        })
    },
    methods: {
        recertification () {
            let url = '../certification/main'
            mpvue.navigateTo({ url })
        }
    }
}
</script>
