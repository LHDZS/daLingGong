<style lang="less" scoped>
.myOddJobs {
    width: 100%;
    background-color: #fff;
    .noOrders {
        width: 100%;
        margin-top: 142rpx;
        text-align: center;
        img {
            width: 269rpx;
            height: 255rpx;
        }
        div {
            margin-top: 70rpx;
            font-size:30rpx;
            font-family:PingFangSC-Regular;
            font-weight:400;
            color:rgba(136,136,136,1);
        }
    }
    .myOddJobs_item {
        width: 100%;
        padding: 0rpx 30rpx;
        box-sizing: border-box;
        .item_title {
            width: 100%;
            line-height: 95rpx;
            font-family:HiraginoSansGB-W6;
            .p1 {
                float: left;
                font-weight: bold;
                font-size:36rpx;
                color:rgba(0,0,0,1);
            }
            .p2 {
                float: right;
                font-size:28rpx;
                color:rgba(9,165,254,1);
            }
        }
        .main {
            width: 100%;
            // height: 206rpx;
            background:rgba(243,249,252,1);
            border-radius:6rpx;
            padding: 15rpx 20rpx;
            box-sizing: border-box;
            position: relative;
            .mian_list {
                width: 100%;
                line-height: 43rpx;
                font-size:26rpx;
                font-family:PingFangSC-Regular;
                font-weight:400;
                color:rgba(102,102,102,1);
                span {
                    color: #999999;
                }
            }
            img {
                position: absolute;
                top: calc(50% - 12rpx);
                right: 20rpx;
                width: 24rpx;
                height: 24rpx;
            }
        }
        .price {
            width: 100%;
            height: 86rpx;
            line-height: 86rpx;
            text-align: right;
            font-size:34rpx;
            font-family:HiraginoSansGB-W3;
            font-weight:normal;
            color:rgba(231,92,68,1);
            border-bottom: 1rpx solid #e4e5ea;
        }
        .button {
            width: 100%;
            height: 116rpx;
            padding: 30rpx 0rpx;
            box-sizing: border-box;
            font-family:HiraginoSansGB-W3;
            font-weight:normal;
            .name {
                float: left;
                font-size:30rpx;
                color:rgba(51,51,51,1);
            }
            .undo {
                float: right;
                width:176rpx;
                height:56rpx;
                line-height: 56rpx;
                text-align: center;
                background:rgba(255,255,255,1);
                border:1rpx solid rgba(204,204,204,1);
                border-radius:28rpx;
                font-size:24rpx;
                color:rgba(51,51,51,1);
            }
        }
    }
}
</style>

<template>
    <div class="myOddJobs clearfix">
        <div>
            <i-tabs :current="current_scroll" scroll @change="handleChangeScroll">
                <i-tab key="tab1" title="全部"></i-tab>
                <i-tab key="tab2" title="待审核"></i-tab>
                <i-tab key="tab3" title="待签约"></i-tab>
                <i-tab key="tab4" title="已签约"></i-tab>
                <i-tab key="tab5" title="进行中"></i-tab>
                <i-tab key="tab6" title="已完成"></i-tab>
                <i-tab key="tab7" title="已驳回"></i-tab>
                <i-tab key="tab8" title="已撤销"></i-tab>
                <i-tab key="tab9" title="已失效"></i-tab>
            </i-tabs>
        </div>
        <div class="clearfix" v-for="(item,key) in myOddJobsArr" :key="key">
            <div class="myOddJobs_item clearfix">
                <div class="item_title clearfix">
                    <div class="p1">国美门店促销员</div>
                    <div class="p2">待审核</div>
                </div>
                <div class="main">
                    <div class="mian_list">
                        发布企业：<span>国美电器</span>
                    </div>
                    <div class="mian_list">
                        工作地址：<span>朝阳区霄云路鹏瑞大厦</span>
                    </div>
                    <div class="mian_list">
                        撤销时间：<span>2019-02-12 09:00</span>
                    </div>
                    <div class="mian_list">
                        开始时间：<span>2019-02-12 09:00</span>
                    </div>
                    <div class="mian_list">
                        结束时间：<span>2019-07-12 18:00</span>
                    </div>
                    <div class="mian_list">
                        发薪时间：<span>2019-07-12 18:00</span>
                    </div>
                    <div class="mian_list">
                        签约时间：<span>2019-07-12 18:00</span>
                    </div>
                    <div class="mian_list">
                        审核时间：<span>2019-07-12 18:00</span>
                    </div>
                    <div class="mian_list">
                        失败原因：<span>不符合企业要求</span>
                    </div>
                    <img src="/static/images/ysjt.png" alt="">
                </div>
                <div class="price">200元/天</div>
                <div class="button">
                    <div class="name">《合同模板名称》.doc</div>
                    <div class="undo">撤销接单</div>
                </div>
            </div>
            <div class="splitter"></div>
        </div>
        
        <div class="noOrders" v-if="myOddJobsArr.length == 0">
            <img src="/static/images/zwdd.png" alt="">
            <div>暂无订单</div>
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            myOddJobsArr:[{},{},{},{}],
            current_scroll: 'tab1'
        }
    },
    onLoad(options) {
        wx.setNavigationBarTitle({
          title:'我的零工',
        })
        this.current_scroll = 'tab' + options.key
        console.log(this.current_scroll)
    },
    mounted () {
        
    },
    methods: {
        handleChangeScroll (detail) {
            this.current_scroll = detail.mp.detail.key
        }
    }
}
</script>
