<style lang="less" scoped>
.mys {
  width: 100%;
  .title {
    width: 100%;
    height: 207rpx;
    background-color: #fff;
    padding: 39rpx 30rpx;
    box-sizing: border-box;
    margin-bottom: 20rpx;
    .title_img {
      float: left;
      width: 128rpx;
      height: 128rpx;
      border-radius: 50%;
      overflow: hidden;
    }
    .title_name {
      float: left;
      margin-left: 39rpx;
      width: 75%;
      height: 88rpx;
      line-height: 88rpx;
      font-size:40rpx;
      font-family:HiraginoSansGB-W3;
      font-weight:normal;
      color:rgba(51,51,51,1);
    }
    .title_renz {
      float: left;
      margin-left: 39rpx;
      width: 142rpx;
      height: 32rpx;
    }
    .title_sz {
      position: absolute;
      top: 86rpx;
      right: 30rpx;
      width: 36rpx;
      height: 36rpx;
    }
  }
  .nav {
    width: 100%;
    height: 207rpx;
    background-color: #fff;
    margin-bottom: 20rpx;
    display: flex;
    .nav_item {
      flex: 1;
      font-size:24rpx;
      font-family:PingFangSC-Regular;
      font-weight:400;
      color:rgba(51,51,51,1);
      text-align: center;
      padding-top: 40rpx;
      box-sizing: border-box;
      img {
        width: 80rpx;
        height: 80rpx;
        margin-bottom: 14rpx;
      }
    }
  }
  .main {
    width: 100%;
    height: 399rpx;
    margin-bottom: 20rpx;
    background-color: #fff;
    .main_items {
      width: 100%;
      font-size:24rpx;
      font-family:PingFangSC-Regular;
      font-weight:400;
      color:rgba(102,102,102,1);
      background-color: #fff;
      border-top: 1rpx solid #e4e5ea;
      .main_item {
        float: left;
        width: 25%;
        height: 148rpx;
        text-align: center;
        padding-top: 30rpx;
        box-sizing: border-box; 
        img {
          width: 46rpx;
          height: 46rpx;
          margin-bottom: 20rpx;
        }
      }
    }
  }
  .kefu {
    width: 100%;
    text-align: center;
    margin-top: 40rpx;
    font-size:24rpx;
    font-family:PingFangSC-Regular;
    font-weight:400;
    color:rgba(191,191,191,1);
  }
}
</style>

<template>
  <div class="mys">
      <div class="title">
        <div class="title_img"><open-data type="userAvatarUrl"></open-data></div>
        <div class="title_name"><open-data type="userNickName"></open-data></div>
        <img class="title_renz" src="/static/images/wrz.png" alt="">
        <img class="title_sz" @click="setupthe" src="/static/images/sz.png" alt="">
      </div>
      <div class="nav">
        <div class="nav_item" v-for="(list,index) in navs" :key="index" @click="navdj(index)">
          <img :src="list.url" alt="">
          <div class="item_text">{{list.name}}</div>
        </div>
      </div>
      <div class="main">
        <i-cell title="我的零工" is-link @click="order(-1)"></i-cell>
        <div class="main_items clearfix">
          <div class="main_item" v-for="(item,key) in workArr" :key="key" @click="order(key)">
            <img :src="item.url" alt="">
            <div>{{item.name}}</div>
          </div>
        </div>
      </div>
      <div class="kefu">客服：4006-798-999</div>
  </div>
</template>

<script>

export default {
  components: {
    
  },
  data () {
    return {
      navs:[{url:'/static/images/wdbc.png',name:'我的报酬'},
      {url:'/static/images/smrz.png',name:'实名认证'},
      {url:'/static/images/wdzl.png',name:'我的资料'},
      {url:'/static/images/wdsc.png',name:'我的收藏'},
      {url:'/static/images/wdxx.png',name:'我的消息'}],
      workArr:[
      {url:'/static/images/dsh.png',name:'待审核'},
      {url:'/static/images/dqy.png',name:'待签约'},
      {url:'/static/images/yqy.png',name:'已签约'},
      {url:'/static/images/jxz.png',name:'进行中'},
      {url:'/static/images/ywc.png',name:'已完成'},
      {url:'/static/images/ybh.png',name:'已驳回'},
      {url:'/static/images/ycx.png',name:'已撤销'},
      {url:'/static/images/yxx.png',name:'已失效'}]
    }
  },
  created () {
    
  },
  methods: {
    order(key) {
      let url = '../myOddJobs/main?key=' + (key+2)
      mpvue.navigateTo({ url })
    },
    setupthe() {
      let url = '../setUpThe/main'
      mpvue.navigateTo({ url })
    },
    navdj(key) {
      let url = ''
      switch (key) {
        case 0:
          url = '../remuneration/main'
          break;
        case 1:
          url = '../certification/main'
          break;
        case 2:
          url = '../myProfile/main'
          break;
        case 3:
          url = '../myCollection/main'
          break;
        case 4:
          url = '../myNews/main'
          break;
      }
      mpvue.navigateTo({ url })
    }
  }
}
</script>
