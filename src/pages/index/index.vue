<template>
  <div class="home">
    <div class="title">
      <div class="location"><img src="/static/images/weizhi.png" alt="">北京</div>
      <div class="input_div">
        <input class="input" type="text" placeholder="搜索职位/公司" placeholder-class="phcolor">
      </div>
      <swiper
        :indicator-dots="indicatorDots"
        :autoplay="autoplay"
        :interval="interval"
        :duration="duration"
        indicator-color="rgba(255, 255, 255, 0.5)"
        indicator-active-color="rgba(255, 255, 255, 1)"
        style="height: 324rpx;"
        >
        <block v-for="(item,key) in imgUrls" :key="key">
          <swiper-item>
            <img :src="item" class="slide-image"/>
          </swiper-item>
        </block>
      </swiper>
    </div>
    <div class="tabs">
      <div v-for="(item,key) in tabsArr" :key="key" class="tabs_item" :style="key == tabKey ? 'color:rgba(9,165,254,1);' : 'color:rgba(51,51,51,1);'" @click="The_dropDown(key)">
        {{item}}
        <i-icon type="unfold" v-if="!type || key != tabKey"/>
        <i-icon type="packup" v-if="type && key == tabKey"/>
      </div>
    </div>
    <div class="content">
      <!-- 综合下拉框 -->
      <div class="drop_down" @click="ShutDown" :animation="dropDown">
        <div class="box" :animation="box">
          <div :class="dropDownKey == index ? 'drop_downin_list' : 'drop_down_list'" v-for="(list,index) in comprehensive" :key="index" @click="choose(index)">
            {{list}}
          <i-icon type="right" v-if="dropDownKey == index" style="float: right;"/>
          </div>
        </div> 
      </div>
      <!-- 零工下拉框 -->
      <div class="drop_down" @click="ShutDown" :animation="dropDown1">
        <div class="box" :animation="box1">
          <div :class="dropDownKey1 == index ? 'drop_downin_list' : 'drop_down_list'" v-for="(list,index) in OddJobs" :key="index" @click="choose1(index)">
            {{list}}
          <i-icon type="right" v-if="dropDownKey1 == index" style="float: right;"/>
          </div>
        </div>
      </div>
      <!-- 筛选 -->
      <div class="drop_down" @click="ShutDown" :animation="dropDown2">
        <div class="box" :animation="box2">
          <div class="text">报酬类型</div>
          <div class="nav">
            <div class="button" :style="rewardKey == key ? 'background:#F3FBFF;border:1rpx solid #09A5FE;color: #09A5FE;' : 'border:1rpx solid #fff;'" v-for="(list,key) in reward" :key="key" @click="rewardKey = key">全部</div>
          </div>
          <div class="text">价格区间</div>
          <div class="nav">
            <div class="input"><input type="number" v-model="minNum" placeholder-class="phcolor" placeholder="最低价"></div>
            <span>-</span>
            <div class="input"><input type="number" v-model="maxNum" placeholder-class="phcolor" placeholder="最高价"></div>
          </div>
          <div class="text">性别要求</div>
          <div class="nav">
            <div class="button" :style="genderKey == key ? 'background:#F3FBFF;border:1rpx solid #09A5FE;color: #09A5FE;' : 'border:1rpx solid #fff;'" v-for="(list,key) in gender" :key="key" @click="genderKey = key">{{list}}</div>
          </div>
          <div class="main">
            <div class="main_left" @click="reset">重置</div>
            <div class="main_right" @click="complete">完成</div>
          </div>
        </div>
      </div>
      <div class="content_item" v-for="(item,key) in contentArr" :key="key" @click="details()">
        <div class="content_title">
          <span class="c_t_left">国美门店促销员</span>
          <span class="c_t_right">200元/天</span>
        </div>
        <div class="content_text"><span>2019.03.21-2019-04.21</span><span>仅限:男</span><span>还缺:1人</span></div>
        <div class="content_div">
          <img class="content_img" src="/static/images/lou.png" alt="">
          <span>北京国美电器有限公司</span>
        </div>
        <div class="content_div">
          <img class="content_img" src="/static/images/di.png" alt="">
          <span>朝阳区-望京</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data () {
    return {
      dropDown: {},//放大动画,
      box:{},
      dropDown1: {},//放大动画,
      box1:{},
      dropDown2: {},//放大动画,
      box2:{},
      // swiper配置
      imgUrls: [
        '/static/images/swiper_img.png',
        '/static/images/swiper_img.png',
        '/static/images/swiper_img.png'
      ],
      indicatorDots: true,
      autoplay: true,
      interval: 5000,
      duration: 1000,
      // 下拉选项卡
      tabsArr:['综合','零工类型','筛选'],
      tabKey:null,
      // 内容区域
      contentArr:[{},{},{}],
      maskSelected:false,
      maskSelected1:false,
      maskSelected2:false,
      type:false,
      dropDownKey:null,
      dropDownKey1:null,
      comprehensive:['最新发布','价格从高到低','价格从低到高','距离从远到近','距离从近到远'],
      OddJobs:['计时','计件','计时加计件'],
      reward:['','',''],
      rewardKey:null,
      gender:['不限','男','女'],
      genderKey:null,
      maxNum:'',
      minNum:'',
      // 
      BoxHeight:null
    }
  },

  components: {
    
  },
  mounted () {
    var that = this
    wx.getLocation({
      type: 'wgs84',
      success(res) {
        const latitude = res.latitude
        const longitude = res.longitude
        const speed = res.speed
        const accuracy = res.accuracy
        // that.loadCity(longitude,latitude)
      }
    })
  },
  methods: {
    speakingShut(i) { 
      
      var _this = this;  
      var animation = wx.createAnimation({  
        duration: 50,
      })  
      animation.height(0).step();

      var animation1 = wx.createAnimation({  
        duration: 50,
      })
      animation1.backgroundColor('rgba(0,0,0,0)').step();
      animation1.height('0rpx').step()
      
      if (i == 0) {
        this.box = animation.export()  
        this.dropDown = animation1.export()
      }else if (i == 1) {
        this.box1 = animation.export()  
        this.dropDown1 = animation1.export()
      }else if (i == 2) {
        this.box2 = animation.export()  
        this.dropDown2 = animation1.export()
      }
    },
    speakingOpen(i) {  
      console.log("动画前.....")
      let boxWidth = ''
      var _this = this;  

      var animation1 = wx.createAnimation({  
        duration: 200,
      })
      animation1.height('100%').step()
      animation1.backgroundColor('rgba(0,0,0,0.5)').step();//修改透明度,放大  

      var animation = wx.createAnimation({
        duration: 100,
      })  
      if (i == 0) {
        boxWidth = '440rpx'
      }else if (i == 1) {
        boxWidth = '264rpx'
      }else if (i == 2) {
        boxWidth = '614rpx'
      }
      animation.height(boxWidth).step();

      if (i == 0) {
        this.box = animation.export()  
        this.dropDown = animation1.export()
      }else if (i == 1) {
        this.box1 = animation.export()  
        this.dropDown1 = animation1.export()
      }else if (i == 2) {
        this.box2 = animation.export()  
        this.dropDown2 = animation1.export()
      }
    },

    loadCity (longitude, latitude) {
      var page = this
      wx.request({
        url: 'https://api.map.baidu.com/geocoder/v2/?ak=您的ak&location=' + latitude + ',' + longitude + '&output=json',
        data: {},
        header: {
          'Content-Type': 'application/json'
        },
        success: function (res) {
          console.log(res);
          // var city = res.data.result.addressComponent.city;
          // page.setData({ currentCity: city });
        },
        fail: function () {
          page.setData({ currentCity: "获取定位失败" });
        },
        
      })
    },
    // 触发显示遮罩层
    The_dropDown(i) {
      if (i == this.tabKey) {
        this.type = !this.type
      }else {
        this.speakingShut(this.tabKey)
        this.tabKey = i
        this.type = true
      }

      if (this.type == false) {
          this.speakingShut(i)
        }else {
          this.speakingOpen(i)
        }
    },
    // 完成
    complete() {
      console.log(this.maxNum)
      console.log(this.minNum)
      this.speakingShut(this.tabKey)
    },
    // 重置
    reset () {
      this.genderKey = null
      this.rewardKey = null
      this.maxNum = ''
      this.minNum = ''
    },
    // 点击关闭遮罩层
    ShutDown () {
      if (this.tabKey != 2) {
        // var timer = setTimeout( () => {  
          this.speakingShut(this.tabKey)
        // }, 200);
      }
      this.type = false
    },
    // 综合
    choose(i) {
      this.dropDownKey = i
    },
    // 零工
    choose1(i) {
      this.dropDownKey1 = i
    },
    details () {
      let url = '../detailsPage/main'
      mpvue.navigateTo({ url })
    }
  },
  created () {
    // let app = getApp()
  }
}
</script>

<style lang="less" scoped>
.home {
  width: 100%;
  height: 100%;
  .title {
    width: 100%;
    height: 324rpx;
    position: relative;
    .input_div {
      z-index: 2019;
      position: absolute;
      top: 18rpx;
      right: 30rpx;
      width:576rpx;
      height:66rpx;
      background:rgba(254,254,255,1);
      border-radius:33rpx;
      .input {
        margin: 0 auto;
        width: 90%;
        height: 100%;
        font-size:24rpx;
        font-family:PingFangSC-Regular;
        font-weight:400;
        color: #333;
      }
    }
    .location {
      z-index: 2019;
      position: absolute;
      top: 30rpx;
      left: 30rpx;
      font-size:28rpx;
      font-family:PingFangSC-Regular;
      font-weight:400;
      color:rgba(255,255,255,1);
      img {
        margin-top: -5rpx;
        margin-right: 10rpx;
        width: 22rpx;
        height: 29rpx;
        vertical-align: middle;
      }
    }
  }
  .tabs {
    width: 100%;
    height: 82rpx;
    display: flex;
    border-bottom: 1rpx solid #e4e5ea;
    background-color: #fff;
    position: relative;
    .tabs_item {
      flex: 1;
      text-align: center;
      line-height: 82rpx;
      font-size:28rpx;
      font-family:PingFangSC-Semibold;
      font-weight:600;
    }
  }
  .content {
    width: 100%;
    min-height: calc(100% - 406rpx);
    background:rgba(242,244,248,1);
    // min-height: 900rpx;
    overflow-y: scroll;
    position: relative;
    .content_item {
      width: 100%;
      height: 243rpx;
      margin-bottom: 20rpx;
      background-color: #fff;
      padding: 31rpx;
      box-sizing: border-box;
      .content_title {
        width: 100%;
        height: 65rpx;
        .c_t_left {
          width: 70%;
          float: left;
          font-size:36rpx;
          font-family:HiraginoSansGB-W3;
          font-weight:normal;
          color:rgba(51,51,51,1);
          overflow: hidden;
          text-overflow:ellipsis;
          white-space: nowrap;
        }
        .c_t_right {
          width: 30%;
          text-align: right;
          float: right;
          font-size:28rpx;
          font-family:HiraginoSansGB-W3;
          font-weight:normal;
          color:rgba(233,91,62,1);
          overflow: hidden;
          text-overflow:ellipsis;
          white-space: nowrap;
        }
      }
      .content_text {
        width: 100%;
        height: 45rpx;
        font-size:24rpx;
        font-family:HiraginoSansGB-W3;
        font-weight:normal;
        color:rgba(164,164,164,1);
        span {
          margin-right: 19rpx; 
        }
      }
      .content_div {
        width: 100%;
        height: 45rpx;
        line-height: 45rpx;
        font-size:26rpx;
        font-family:HiraginoSansGB-W3;
        font-weight:normal;
        color:rgba(153,153,153,1);
        .content_img {
          margin-top:-5rpx;
          width: 22rpx;
          height: 24rpx;
          vertical-align: middle;
          margin-right: 9rpx;
        }
      }
    }
    .drop_down {
      width: 100%;
      height: 0rpx;
      position: absolute;
      top: 0;
      left: 0;
      background-color: rgba(0,0,0,0);
      .box {
        width: 100%;
        height: 0rpx;
        background-color: #fff;
        overflow: hidden;
        .drop_down_list {
          width: 100%;
          height: 88rpx;
          line-height: 88rpx;
          font-size:28rpx;
          font-family:HiraginoSansGB-W3;
          font-weight:normal;
          text-align: left;
          color:rgba(153,153,153,1);
          padding: 0 30rpx;
          background-color: #fff;
          box-sizing: border-box;
        }
        .drop_downin_list {
          width: 100%;
          height: 88rpx;
          line-height: 88rpx;
          font-size:28rpx;
          font-family:HiraginoSansGB-W3;
          font-weight:normal;
          text-align: left;
          color:rgba(9,165,254,1);
          padding: 0 30rpx;
          box-sizing: border-box;
          background:rgba(242,244,248,1);

        }
        .text {
          float: left;
          width: 100%;
          height: 87rpx;
          line-height: 87rpx;
          font-size:28rpx;
          font-family:HiraginoSansGB-W6;
          font-weight: bold;
          color:rgba(51,51,51,1);
          background-color: #fff;
          padding-left: 30rpx;
          box-sizing: border-box;
        }
        .nav {
          overflow: hidden;
          width: 100%;
          padding-left:30rpx;
          padding-bottom: 25rpx;
          background-color: #fff;
          box-sizing: border-box;
          color: #ccc;
          .button {
            float: left;
            width: 160rpx;
            height: 62rpx;
            margin-right: 30rpx;
            line-height: 62rpx;
            text-align: center;
            background:rgba(245,245,245,1);
            border-radius:31rpx;
            font-size:24rpx;
            font-family:HiraginoSansGB-W3;
            font-weight:normal;
            color:rgba(51,51,51,1);
          }
          span {
            float: left;
            width: 50rpx;
            text-align: center;
            color:rgba(102,102,102,1);
          }
          .input {
            float: left;
            width:320rpx;
            // height:62rpx;
            line-height: 62rpx;
            text-align: center;
            background:rgba(245,245,245,1);
            border-radius:31rpx;
            font-size:24rpx;
            font-family:HiraginoSansGB-W3;
            font-weight:normal;
            input {
              height: 100%;
              color: #333;
            }
          }
        }
        .main {
          width: 100%;
          height: 100rpx;
          font-family:HiraginoSansGB-W3;
          font-weight:normal;
          font-size:34rpx;
          overflow: hidden;
          border-top: 1rpx solid #e4e5ea;
          .main_left {
            float: left;
            width: 50%;
            height: 100%;
            line-height: 100rpx;
            text-align: center;
            color:rgba(51,51,51,1);
          }
          .main_right {
            float: right;
            width: 50%;
            height: 100%;
            line-height: 100rpx;
            text-align: center;
            background-color: #09A5FE;
            color:#fff;
          }
        }
      }
    }
  }
}
</style>

