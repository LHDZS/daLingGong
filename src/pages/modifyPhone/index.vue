<style lang="less" scoped>
.modifyPhone {
    width: 100%;
    canvas {
        margin-top: 32rpx;
        margin-right: 30rpx;
        width: 160rpx;
        height: 48rpx;
        border-radius: 14rpx;
        float: right;
    }
    .mPhone_item {
        width: 100%;
        height: 111rpx;
        line-height: 111rpx;
        border-top: 1rpx solid #e4e5ea;
        font-size:30rpx;
        font-family:PingFangSC-Regular;
        font-weight:400;
        color:rgba(204,204,204,1);
        img {
            float: left;
            margin-top: 40rpx;
            margin-left: 31rpx;
            width: 36rpx;
            height: 36rpx;
        }
        input {
            width: 60%;
            float: left;
            height: 111rpx;
            line-height: 111rpx;
            padding-left: 20rpx;
            color: #333;
        }
        .SMS {
            float: right;
            margin-top: 31rpx;
            margin-right: 30rpx;
            width:160rpx;
            height:48rpx;
            line-height: 48rpx;
            text-align: center;
            border:1rpx solid rgba(9,165,254,1);
            border-radius:6rpx;
            font-size:26rpx;
            font-family:PingFangSC-Regular;
            font-weight:400;
            color:rgba(9,165,254,1);
        }
    }
    .The_divider {
        width:100%;
        height:1rpx;
        background:rgba(228,229,234,1);
    }
    .ModifyThe {
        margin: 0 auto;
        margin-top: 64rpx;
        width:598rpx;
        height:86rpx;
        line-height: 86rpx;
        text-align: center;
        background:rgba(74,189,252,0.29);
        border-radius:43rpx;
        font-size:35rpx;
        font-family:HiraginoSansGB-W3;
        font-weight:normal;
        color: #fff;
    }
}
</style>

<style lang="less">
page {
    background-color: #fff;
}
</style>


<template>
    <div class="modifyPhone">
        <div class="mPhone_item">
            <img src="/static/images/sj.png" alt="">
            <input type="number" placeholder="请输入新手机号" placeholder-class="phcolor" maxlength="11">
        </div>
        <div class="mPhone_item">
            <img src="/static/images/dxyzm.png" alt="">
            <input type="number" placeholder="请输入短信验证码" placeholder-class="phcolor">
            <div class="SMS">短信验证码</div>
        </div>
        <div class="mPhone_item">
            <img src="/static/images/yzm.png" alt="">
            <input type="number" placeholder="请输入验证码" placeholder-class="phcolor" maxlength="4">
            <canvas id="canvas" canvas-id="canvas" @click='change'></canvas>
        </div>
        <div class="The_divider"></div>
        <div class="ModifyThe">修改</div>
    </div>
</template>

<script>
var ctx;
export default {
    data () {
        return {
            text: '',
            value5:'',
            canvasWidth: null,
            canvasHeight: null,
        }
    },
    onLoad() {
        wx.setNavigationBarTitle({
          title:'修改绑定手机号',
        })
    },
    created () {

    },
    mounted () {
        var that = this;
        this.drawPic(that);  
    },
    methods: {
        randomNum(min, max) {
            return Math.floor(Math.random() * (max - min) + min);
        },
        /**生成一个随机色**/
        randomColor(min, max) {
            var r = this.randomNum(min, max);
            var g = this.randomNum(min, max);
            var b = this.randomNum(min, max);
            return "rgb(" + r + "," + g + "," + b + ")";
        },
        
        /**绘制验证码图片**/
        drawPic(that) {
            ctx = wx.createCanvasContext('canvas');
            /**绘制背景色**/
            ctx.fillStyle = this.randomColor(180, 240); //颜色若太深可能导致看不清
            var obj = wx.createSelectorQuery()
            obj.select('#canvas').boundingClientRect(function (rect) {        
                this.canvasWidth = rect.width
                this.canvasHeight = rect.height
                ctx.fillRect(0, 0, rect.width, rect.height)
                /**绘制文字**/
                var arr;
                let text = '';
                var str = 'ABCEFGHJKLMNPQRSTWXY123456789';
                for (var i = 0; i < 4; i++) {
                    var txt = str[that.randomNum(0, str.length)];
                    ctx.fillStyle = that.randomColor(50, 160); //随机生成字体颜色
                    ctx.font = that.randomNum((this.canvasHeight/1.3), this.canvasHeight) + 'px SimHei'; //随机生成字体大小
                    var x = (this.canvasHeight/5) + i * (this.canvasHeight/1.3);
                    var y = that.randomNum((this.canvasHeight/1.3), this.canvasHeight);
                    var deg = that.randomNum(-(this.canvasHeight/1.3), (this.canvasHeight/1.3));
                    //修改坐标原点和旋转角度
                    ctx.translate(x, y);
                    ctx.rotate(deg * Math.PI / 180);
                    ctx.fillText(txt, 5, 0);
                    text = text + txt;
                    //恢复坐标原点和旋转角度
                    ctx.rotate(-deg * Math.PI / 180);
                    ctx.translate(-x, -y);
                }
                /**绘制干扰线**/
                for (var i = 0; i < 4; i++) {
                    ctx.strokeStyle = that.randomColor(40, 180);
                    ctx.beginPath();
                    ctx.moveTo(that.randomNum(0, this.canvasWidth), that.randomNum(0, this.canvasHeight));
                    ctx.lineTo(that.randomNum(0, this.canvasWidth), that.randomNum(0, this.canvasHeight));
                    ctx.stroke();
                }
                /**绘制干扰点**/
                for (var i = 0; i < 20; i++) {
                    ctx.fillStyle = that.randomColor(0, 255);
                    ctx.beginPath();
                    ctx.arc(that.randomNum(0, this.canvasWidth), that.randomNum(0, this.canvasHeight), 1, 0, 2 * Math.PI);
                    ctx.fill();
                }
                ctx.draw(false, function() {
                    that.text = text
                });
            }).exec()
        },
        change () {
            var that = this;
            this.drawPic(that);
        }
    }
}
</script>
