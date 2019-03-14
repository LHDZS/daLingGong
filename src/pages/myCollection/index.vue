<style lang="less" scoped>
.myCollection {
    width: 100%;
    height: 100%;
    background-color: #fff;
    .mc_items {
        width: 100%;
        .mc_item {
            width: 100%;
            // height: 291rpx;
            overflow: hidden;
            padding: 0 31rpx;
            padding-bottom: 22rpx;
            box-sizing: border-box;
            background-color: #fff;
            .mcitem_left {
                width: 75%;
                float: left;
                font-family:HiraginoSansGB-W3;
                font-weight:normal;
                overflow: hidden;
                .title {
                    margin-top: 25rpx;
                    font-size:36rpx;
                    color:rgba(51,51,51,1);
                }
                .price {
                    margin-top: 18rpx;
                    font-size:28rpx;
                    color:rgba(233,91,62,1);
                }
                .time {
                    margin-top: 17rpx;
                    margin-bottom: 15rpx;
                    font-size:24rpx;
                    color:rgba(164,164,164,1);
                }
                .text {
                    width: 100%;
                    height: 45rpx;
                    line-height: 45rpx;
                    font-size:26rpx;
                    font-family:HiraginoSansGB-W3;
                    font-weight:normal;
                    color:rgba(153,153,153,1);
                    .text_img {
                        margin-top:-5rpx;
                        width: 22rpx;
                        height: 24rpx;
                        vertical-align: middle;
                        margin-right: 9rpx;
                    }
                }
            }
            .mcitem_right {
                float: right;
                width: 22%;
                text-align: center;
                font-family:HiraginoSansGB-W3;
                font-weight:normal;
                img {
                    margin-top: 30rpx;
                    width: 34rpx;
                    height: 32rpx;
                }
                .text {
                    font-size:22rpx;
                    color:rgba(153,153,153,1);
                }
                .details {
                    margin-top: 120rpx;
                    width: 148rpx;
                    height: 48rpx;
                    line-height: 48rpx;
                    text-align: center;
                    border:1px solid rgba(216,216,216,1);
                    border-radius:24rpx;
                    font-size:24rpx;
                    color:rgba(102,102,102,1);
                }
            }
        }
    }
}
</style>

<template>
    <div class="myCollection">
        <div class="The_divider"></div>
        <div v-if="collectionArr.length != 0">
            <div class="mc_items" v-for="(item,key) in collectionArr" :key="key">
                <div class="mc_item">
                    <div class="mcitem_left">
                        <div class="title">国美门店促销员</div>
                        <div class="price">200元/天</div>
                        <div class="time">2019.03.21-2019-04.21</div>
                        <div class="text">
                            <img class="text_img" src="/static/images/lou.png" alt="">
                            <span>北京国美电器有限公司</span>
                        </div>
                        <div class="text">
                            <img class="text_img" src="/static/images/di.png" alt="">
                            <span>朝阳区-望京</span>
                        </div>
                    </div>
                    <div class="mcitem_right">
                        <img :src="type ? '/static/images/sch.png' : '/static/images/scq.png'" alt="" @click="Collection">
                        <div class="text">120人收藏</div>
                        <div class="details" @click="jump">查看详情</div>
                    </div>
                </div>
                <div class="splitter"></div>
            </div>
        </div>
        
        <div class="prompt" v-if="collectionArr.length == 0">
            <img src="/static/images/fk.png" alt="">
            <div class="text">亲，您还没有收藏哦～</div>
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
           collectionArr:[{},{}],
           type: false
        }
    },
    onLoad() {
        wx.setNavigationBarTitle({
          title:'我的收藏',
        })
    },
    mounted () {
        
    },
    methods: {
        jump () {
            let url = '../oddJobsDetails/main'
            mpvue.navigateTo({ url })
        },
        Collection () {
            this.type = !this.type
        }
    }
}
</script>
