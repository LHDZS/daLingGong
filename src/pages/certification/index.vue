<style lang="less" scoped>
.certification {
    width: 100%;
    .title {
        width: 100%;
        height: 90rpx;
        font-size:24rpx;
        font-family:PingFangSC-Regular;
        font-weight:400;
        color:rgba(153,153,153,1);
        padding: 0 30rpx;
        padding-top: 15rpx;
        box-sizing: border-box;
        background:rgba(242,244,248,1);
        span {
            display: inline-block;
            width:8rpx;
            height:8rpx;
            margin-bottom: 6rpx;
            background:rgba(246,132,31,1);
            border-radius:50%;
        }
    }
    .main {
        width: 100%;
        .main_img {
            margin: 0 auto;
            margin-top: 99rpx;
            width:445rpx;
            height:268rpx;
            background:rgba(255,255,255,1);
            border:1rpx solid rgba(229,229,229,1);
            border-radius:12rpx;
            overflow: hidden;
        }
        .main_photo {
            margin: 0 auto;
            margin-top: 99rpx;
            width:445rpx;
            height:268rpx;
            background:rgba(255,255,255,1);
            border:1rpx solid rgba(229,229,229,1);
            border-radius:12rpx;
            padding: 21rpx 37rpx 0rpx 40rpx;
            box-sizing: border-box;
            img {
                width: 386rpx;
                height: 175rpx;
            }
            .text {
                width: 100%;
                text-align: center;
                font-size:30rpx;
                font-family:PingFangSC-Regular;
                font-weight:400;
                color:rgba(51,51,51,1);
            }
        }
    }
    .submit {
        margin: 0 auto;
        margin-top: 180rpx;
        width:566rpx;
        height:84rpx;
        line-height: 84rpx;
        text-align: center;
        background:rgba(9,165,254,0.11);
        border-radius:42rpx;
        font-size:38rpx;
        font-family:SourceHanSansCN-Regular;
        font-weight:400;
        color:rgba(255,255,255,1);
    }
    .submitOn {
        margin: 0 auto;
        margin-top: 180rpx;
        width:566rpx;
        height:84rpx;
        line-height: 84rpx;
        text-align: center;
        background:#09A5FE;
        border-radius:42rpx;
        font-size:38rpx;
        font-family:SourceHanSansCN-Regular;
        font-weight:400;
        color:rgba(255,255,255,1);
    }
}
</style>

<style lang="less">
page {
    background-color: #fff;
}
</style>


<template>
    <div class="certification">
        <div class="title">
            <span></span>
            实名认证成功，才可以快速接单，请按规定上传身份证照片，我们将严格保证您的信息安全。
        </div>
        <div class="main">
            <div class="main_img" v-if="idcardIsImg" @click="handleOpen1(1)">
                <img :src="idcardIsImg" alt="">
            </div>
            <div class="main_img" v-if="idcardTheImg" @click="handleOpen1(2)">
                <img :src="idcardTheImg" alt="">
            </div>
            <div class="main_photo" v-if="!idcardIsImg" @click="handleOpen1(1)">
                <img src="/static/images/sfzz.png" alt="">
                <div class="text">点击拍摄/上传人像面</div>
            </div>
            <div class="main_photo" v-if="!idcardTheImg" @click="handleOpen1(2)">
                <img src="/static/images/sfzb.png" alt="">
                <div class="text">点击拍摄/上传国徽面</div>
            </div>
        </div>
        <div :class="idcardIsImg && idcardTheImg ? 'submitOn' : 'submit'" @click="submit">提交</div>
        <i-action-sheet :visible="visible1" :actions="actions1" show-cancel @cancel="handleCancel1" @click="handleClickItem1" />
    </div>
</template>

<script>
export default {
    data () {
        return {
            visible1: false,
            actions1: [
                {
                    name: '上传',
                    icon: 'dynamic',
                    openType: 'dynamic'
                },
                {
                    name: '拍摄',
                    icon: 'camera',
                    openType: 'camera'
                }
            ],
            idcardIsImg:'',
            idcardTheImg:'',
            imgNum: null
        }
    },
    onLoad(options) {
        wx.setNavigationBarTitle({
          title:'身份认证',
        })
        if (options.id == 1) {
            this.idcardIsImg = options.src
        }else {
            this.idcardTheImg = options.src
        }
        console.log(options)
    },
    mounted () {

    },
    methods:{
        submit () {
            if (this.idcardIsImg && this.idcardTheImg) {
                let url = '../certificationPrompt/main'
                mpvue.navigateTo({ url })
            }
        },
        handleOpen1 (val) { 
            this.visible1 = true 
            this.imgNum = val
        },
        handleCancel1 () {
            this.visible1 = false 
        },
        handleClickItem1 (detail) {
            let url = ''
            let that = this
            switch (detail.mp._relatedInfo.anchorTargetText) {
                case '上传':
                    wx.chooseImage({
                        count: 1,
                        sizeType: ['original', 'compressed'],
                        sourceType: ['album', 'camera'],
                        success(res) {
                            console.log(res)
                            // tempFilePath可以作为img标签的src属性显示图片
                            const tempFilePaths = res.tempFilePaths[0]
                            console.log(tempFilePaths)
                            if (that.imgNum == 1) {
                                that.idcardIsImg = tempFilePaths
                            }else {
                                that.idcardTheImg = tempFilePaths
                            }
                            that.visible1 = false 
                        }
                    })
                    console.log('上传')
                    break;
                case '拍摄':
                    url = '../photograph/main?id=' + this.imgNum
                    break;
            }
            if (url != '') {
                mpvue.navigateTo({ url })
                this.visible1 = false 
            }
        },
    }
}
</script>
