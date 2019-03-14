<template>
    <div class="photograph">
        <camera v-if='isShowCamera' ref="camera" device-position="back" flash="off" :style="{'width':'100%', 'height':'800rpx'}">
        
            <cover-view class='camerabgImage-view'>
            <cover-view class="img_kuang"></cover-view>
        
            </cover-view>
        </camera>
        <div class="camera_button">
            <!-- <i-button type="primary" i-class="cambut_list" @click="takePhotoAction">返回</i-button> -->
            <!-- <div class="zhanwei"></div> -->
            <i-button type="primary" i-class="cambut_list" @click="takePhotoAction">拍摄</i-button>
        </div>

        <div class="photo_text">拍摄身份证人像面</div>
        <div class="photo_span">请将证件置于取景框内</div>

        <div style="witdh:100%;margin-top:999rpx">
            <canvas v-if="isShowImage" canvas-id="image-canvas" :style="{'width': '100%', 'height': '800rpx'}"></canvas>
        </div>
        <!-- <div style="text-align:center;">
            <img class="image" mode="widthFix" :src="image">
        </div> -->
    </div>
</template>

<style lang="less" scoped>
    .image {
        height: auto;
        // width: 100%;
        // height: 200rpx;
    }
    .photograph {
        width: 100%;
        height: 100%;
        .camera_button {
            width: 100%;
            overflow: hidden;
            text-align: center;
            ._i-button {
                display: inline-block;
                width: 90%;
            }
        }
        .photo_text {
            width: 100%;
            margin-top: 68rpx;
            text-align: center;
            font-size:42rpx;
            font-family:HiraginoSansGB-W6;
            font-weight:normal;
            color:rgba(0,0,0,1);
        }
        .photo_span {
            width: 100%;
            margin-top: 26rpx;
            text-align: center;
            font-size:30rpx;
            font-family:HiraginoSansGB-W3;
            font-weight:normal;
            color:rgba(102,102,102,1);
        }
    }
    .img_text {
        width: 100rpx;
        height: 50rpx;
        background-color: red;
    }
    .img_kuang {
        margin: 0 auto;
        margin-top: 100rpx;
        width:686rpx;
        height:434rpx;
        background:rgba(255,255,255,0.33);
        border:2rpx solid rgba(255,255,255,1);
        border-radius:34rpx;
    }
    .camerabgImage-view{
      height: 100%;
      width: 100%;
      position:absolute;
    }
    /* 底部 */
    .camerabotton-view{
      height: 200rpx;
      width: 100%;
      position:absolute;
    
      display: flex;
      justify-content: space-around;
      align-items: center;
    }
 </style>

<script>
export default {
    data () {
        return {
            src:'',
            isShowCamera: false,
            width: 10,
            height: 10,
            src: "",
            image: "",
            skipphotoStatus: "0",// 1跳过 0没有跳过
            isShowImage: false,
            isIphoneX:true,
            url:'',
            path:null,
            imgNum: null

        }
    },
    onLoad(options) {
        wx.setNavigationBarTitle({
          title:'身份认证',
        })
        this.imgNum = options.id
    },
    mounted () {
    // requireJs.adaptionIphoneX(this);
 
    this.ctx = wx.createCameraContext()
    //   wx.createCameraContext()
    var that = this
    wx.authorize({
      scope: 'scope.camera',
      success: function (res) {
          that.isShowCamera = true
      },
      fail: function (res) {
        console.log("" + res);
        wx.showModal({
          title: '请求授权您的摄像头',
          content: '如需正常使用此小程序功能，请您按确定并在设置页面授权用户信息',
          confirmText: '确定',
          success: res => {
            if (res.confirm) {
              wx.openSetting({
                success: function (res) {
                  console.log('成功');
                  console.log(res);
                  if (res.authSetting['scope.camera']) { //设置允许获取摄像头
                    console.log('设置允许获取摄像头')
                    wx.showToast({
                      title: '授权成功',
                      icon: 'success',
                      duration: 1000
                    })
                    
                      that.isShowCamera = true
                    
 
                  } else { //不允许
                    wx.showToast({
                      title: '授权失败',
                      icon: 'none',
                      duration: 1000
                    })
                    
                    console.log('不允许')
                    
                  }
                }
              })
            } else { //取消
              wx.showToast({
                title: '授权失败',
                icon: 'none',
                duration: 1000
              })
             
            console.log('已取消')
              
            }
          }
        })
 
      }
    })
    },
    methods: {
        takePhotoAction: function() {
            var that = this
            that.ctx.takePhoto({
                quality: 'high', //高质量
                success: (res) => {
                    // console.log(res)
                    that.loadTempImagePath(res.tempImagePath);
                },
            })
        },
        loadTempImagePath: function(options) {
            var that = this
            that.path = options
            wx.getSystemInfo({
            success: function(res) {
                // 矩形的位置
                var image_x = 10
                var image_y = 90
                var image_width = 696
                var image_height = 444
                var canvas_width = wx.getSystemInfoSync().windowWidth
                var canvas_height = wx.getSystemInfoSync().windowHeight
                wx.getImageInfo({
                    src: that.path,
                    success: function(res) {
                        that.isShowImage = true
                        that.canvas = wx.createCanvasContext("image-canvas", that)
                        //过渡页面中，图片的路径坐标和大小
                        that.canvas.drawImage(that.path, 0, 0, canvas_width, 640)
                        wx.showLoading({
                            title: '数据处理中...',
                            icon: 'loading',
                            duration: 10000
                        })
                        // 这里有一些很神奇的操作,总结就是MD拍出来的照片规格居然不是统一的过渡页面中，对裁剪框的设定
                        that.canvas.setStrokeStyle('black')
                        that.canvas.strokeRect(image_x, image_y, image_width, image_height)
                        // that.canvas.draw()
                        that.canvas.draw(false, 
                            setTimeout(function() {
                                mpvue.canvasToTempFilePath({ //裁剪对参数
                                    canvasId: "image-canvas",
                                    x: image_x, //画布x轴起点
                                    y: image_y, //画布y轴起点
                                    width: canvas_width, //画布宽度
                                    height: 800, //画布高度
                                    destWidth: image_width, //输出图片宽度
                                    destHeight: image_height, //输出图片高度
                                    success: function(res) {
                                        that.image = res.tempFilePath
                                    
                                        //清除画布上在该矩形区域内的内容。
                                        that.isShowImage = false
                                        // that.canvas.clearRect(0, 0, that.data.width, that.data.height)
                                        // that.canvas.drawImage(res.tempFilePath, image_x, image_y, image_width, image_height)
                                        // that.canvas.draw()
                                        wx.hideLoading()
                                        let url = '../certification/main?src=' + res.tempFilePath + '&&id=' + that.imgNum
                                        console.log(url)
                                        mpvue.redirectTo({ url })
                                        //在此可进行网络请求
                                        // PublicJS.drivinglicenseUpload(res.tempFilePath, that.uploadFile);
                                    },
                                    fail: function(e) {
                                        console.log(e)
                                        wx.hideLoading()
                                        wx.showToast({
                                            title: '出错啦...',
                                            icon: 'loading'
                                            })
                                        if (this.skipphotoStatus == 1) {
                                            // wx.redirectTo({
                                            // url: 'addCarInfo/addCarInfo',
                                            // })
                                        } else {
                                            // wx.navigateBack({
                                            // delta: 1
                                            // });
                                        }
                                    }
                                },that);
                            }, 200)
                        );
                        
                }
                })
            }
            })
        },
        uploadFile: function(data) {},
        takePhoto() {
            console.log("????????")
            const ctx = wx.createCameraContext()
            ctx.takePhoto({
                quality: 'high',
                success: (res) => {
                    console.log(res)
                    this.src= res.tempImagePath
                }
            })
        }
    }
}
</script>
