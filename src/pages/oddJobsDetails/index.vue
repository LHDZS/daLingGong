<style lang="less" scoped>
.oddJobsDetails {
    width: 100%;
    height: 100%;
    .title {
        width: 100%;
        height: 272rpx;
        padding: 29rpx;
        box-sizing: border-box;
        margin-bottom: 20rpx;
        background-color: #fff;
        .content_title {
            width: 100%;
            height: 65rpx;
            line-height: 65rpx;
            .c_t_left {
            width: 70%;
            float: left;
            font-size:42rpx;
            font-family:HiraginoSansGB-W6;
            font-weight:normal;
            color:rgba(0,0,0,1);
            overflow: hidden;
            text-overflow:ellipsis;
            white-space: nowrap;
            }
            .c_t_right {
            width: 30%;
            text-align: right;
            float: right;
            font-size:34rpx;
            font-family:HiraginoSansGB-W3;
            font-weight:normal;
            color:rgba(231,92,68,1);
            overflow: hidden;
            text-overflow:ellipsis;
            white-space: nowrap;
            }
        }
        .dp_t_js {
            width: 100%;
            margin-top: 15rpx;
            .js {
                width: 112rpx;
                height: 40rpx;
                line-height: 40rpx;
                text-align: center;
                background:rgba(236,248,255,1);
                border-radius:3rpx;
                font-size:24rpx;
                font-family:HiraginoSansGB-W3;
                font-weight:normal;
                color:rgba(51,51,51,1);
            }
        }
        .dp_text {
            height: 30rpx;
            line-height: 30rpx;
            margin-top: 20rpx;
            font-size:26rpx;
            font-family:HiraginoSansGB-W3;
            font-weight:normal;
            color:rgba(102,102,102,1);
            span {
                color: #999999;
            }
            .dp_text_left {
                width: 80%;
                float: left;
                overflow: hidden;
                text-overflow:ellipsis;
                white-space: nowrap;
            }
            .dp_text_right {
                width: 20%;
                text-align: right;
                float: right;
                color:rgba(9,165,254,1);
                overflow: hidden;
                text-overflow:ellipsis;
                white-space: nowrap;
            }
        }
    }
    .tag_title {
        width: 100%;
        height: 68rpx;
        line-height: 68rpx;
        font-size:30rpx;
        font-family:PingFangSC-Regular;
        font-weight:400;
        color:rgba(34,34,34,1);
        box-sizing: border-box;
        border-bottom: 1rpx solid #F2F5F9;
    }
    .tag1 {
        width: 100%;
        height: 205rpx;
        margin-bottom: 20rpx;
        background-color: #fff;
        padding: 0rpx 30rpx;
        box-sizing: border-box;
        .tag_main {
            margin-top: 40rpx;
            width: 100%;
            height: 56rpx;
            line-height: 56rpx;
            font-size:26rpx;
            font-weight:400;
            .tag_main_time {
                width: 23%;
                float: left;
                font-family:PingFangSC-Regular;
                color:rgba(51,51,51,1);
            }
            .tag_main_img {
                float: left;
                width: 372rpx;
                height: 56rpx;
                text-align: center;
                font-family:MicrosoftYaHei;
                color:rgba(9,165,254,1);
                background: url('data:image/png;base64,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');
                background-size: 100% 100%;
            }
        }
    }
    .tag2 {
        width: 100%;
        height: 208rpx;
        padding: 0rpx 30rpx;
        box-sizing: border-box;
        background-color: #fff;
        margin-bottom: 20rpx;
        .tag2_text {
            width: 100%;
            font-size:26rpx;
            font-family:PingFangSC-Regular;
            font-weight:400;
            color:rgba(51,51,51,1);
            margin-top: 20rpx;
            .t2tx_left {
                display: inline-block;
                width: 80%;
                text-align: left;
            }
            .t2tx_right {
                display: inline-block;
                width: 20%;
                text-align: right;
            }
        }
    }
    .tag3 {
        width: 100%;
        height: 144rpx;
        background-color: #fff;
        padding: 0rpx 30rpx;
        box-sizing: border-box;
        margin-bottom: 20rpx;
        .tag3_text {
            width:100%;
            margin-top: 13rpx;
            font-size:28rpx;
            font-family:PingFangSC-Regular;
            font-weight:400;
            color:rgba(102,102,102,1);
        }
    }
    .tag4 {
        width: 100%;
        height: 286rpx;
        background-color: #fff;
        padding: 0rpx 30rpx;
        box-sizing: border-box;
        .tag4_main {
            width: 100%;
            margin-top: 29rpx;
            div {
                line-height: 45rpx;
                font-size:26rpx;
                font-family:PingFangSC-Regular;
                font-weight:400;
                color: #666;
                margin-top: 10rpx;
                span {
                    color: #999999;
                }
            }
        }
    }
}
</style>

<template>
    <div class="oddJobsDetails">
        <div class="title">
            <div class="content_title">
                <span class="c_t_left">国美门店促销员</span>
                <span class="c_t_right">200元/天</span>
            </div>
            <div class="dp_t_js">
                <div class="js">
                    <i-icon type="time" style="color:rgba(9,165,254,1);font-size:22rpx;"/>
                    计时
                </div>
            </div>
            <div class="dp_text">发布企业：<span>国美电器</span></div>
            <div class="dp_text">
                <div class="dp_text_left">工作地址：<span>朝阳区霄云路鹏瑞大厦</span></div>
                <div class="dp_text_right">距您3.6km</div>
            </div>
        </div>
        <div class="tag1">
            <div class="tag_title">工作时间</div>
            <div class="tag_main">
                <div class="tag_main_time" style="text-align: left;">2017.04.01</div>
                <div class="tag_main_img">白班 10:00-19:00</div>
                <div class="tag_main_time" style="text-align: right;">2018.12.19</div>
            </div>
        </div>
        <div class="tag2">
            <div class="tag_title">招工人数</div>
            <div class="tag2_text">
                <div class="t2tx_left">共需要</div>
                <div class="t2tx_right">45人</div>
            </div>
            <div class="tag2_text">
                <div class="t2tx_left">已接单人数</div>
                <div class="t2tx_right">4人</div>
            </div>
        </div>
        <div class="tag3">
            <div class="tag_title">招工要求</div>
            <div class="tag3_text">男，18-25岁，有相关经验优先。</div>
        </div>
        <div class="tag4">
            <div class="tag_title">订单信息</div>
            <div class="tag4_main">
                <div>订单编号：<span>0989889999038499</span></div>
                <div>订单创建时间：<span>2019-02-16 18:00</span></div>
                <div>审核通过时间：<span>2019-02-16 18:00</span></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    
}
</script>
