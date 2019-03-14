<script>
export default {
  created () {
    // 调用API从本地缓存中获取数据
    /*
     * 平台 api 差异的处理方式:  api 方法统一挂载到 mpvue 名称空间, 平台判断通过 mpvuePlatform 特征字符串
     * 微信：mpvue === wx, mpvuePlatform === 'wx'
     * 头条：mpvue === tt, mpvuePlatform === 'tt'
     * 百度：mpvue === swan, mpvuePlatform === 'swan'
     * 支付宝(蚂蚁)：mpvue === my, mpvuePlatform === 'my'
     */
  },
}
</script>

<style lang="less">
page {
  height: 100%;
  background:#f7f8fa;
}
page::before{
    content: '';
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 2rpx;
    background-color: #eaebee;
    z-index: 9999;
}
page::after{
    content: '';
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 2rpx;
    background-color: #eaebee;
    z-index: 9999;
}
.container {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  padding: 200rpx 0;
  box-sizing: border-box;
}
/* this rule will be remove */
* {
  transition: width 2s;
  -moz-transition: width 2s;
  -webkit-transition: width 2s;
  -o-transition: width 2s;
}
img {
  width: 100%;
  height: 100%;
}
.phcolor {
  color:#ccc;
}
.clearfix:after{
  content:"";
  display:block;
  visibility:hidden;
  clear:both;
  height:0;
}
.clearfix{ 
  zoom:1;
}
.The_divider {
  width:100%;
  height:1rpx;
  background:rgba(228,229,234,1);
}
.splitter {
  width: 100%;
  height: 20rpx;
  background-color: #f2f4f8;
}
.prompt {
  margin: 0 auto;
  padding-top: 230rpx;
  width: 342rpx;
  height: 337rpx;
  img {
    width: 100%;
    height: 255rpx;
  }
  .text {
    width: 100%;
    text-align: center;
    margin-top: 60rpx;
    font-size:30rpx;
    font-family:PingFangSC-Regular;
    font-weight:400;
    color:rgba(136,136,136,1);
  }
}
</style>
