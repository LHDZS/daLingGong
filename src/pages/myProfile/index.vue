<style lang="less" scoped>
.myProfile {
    width: 100%;
    height: 100%;
    background-color: #fff;
    .nav_item {
        width: 100%;
        height: 92rpx;
        line-height: 92rpx;
        font-size:30rpx;
        font-family:PingFangSC-Regular;
        font-weight:400;
        color:rgba(51,51,51,1);
        border-top: 1rpx solid #e4e5ea;
        padding: 0rpx 40rpx;
        box-sizing: border-box;
        span {
            float: left;
        }
        div {
            float: left;
            width: 88%;
            height: 100%;
            line-height: 92rpx;
            font-size:30rpx;
            font-family:PingFangSC-Regular;
            font-weight:400;
            color:rgba(102,102,102,1);
            padding-left: 91rpx;
            box-sizing: border-box;
        }
        input {
            width: 60%;
            height: 100%;
            line-height: 92rpx;
            font-size:30rpx;
            font-family:PingFangSC-Regular;
            font-weight:400;
            color:rgba(102,102,102,1);
            padding-left: 91rpx;
            box-sizing: border-box;
        }
        .icon {
            width: 18rpx;
            height: 28rpx;
            vertical-align: middle;
            margin-top: -5rpx;
        }
        .headPortrait {
            margin-top: 26rpx;
            margin-left: 90rpx;
            width: 76rpx;
            height: 76rpx;
        }   
    }
    .formSubmit {
        margin: 0 auto;
        margin-top: 122rpx;
        width:566rpx;
        height:84rpx;
        line-height: 84rpx;
        text-align: center;
        background:rgba(9,165,254,1);
        border-radius:42rpx;
        font-size:38rpx;
        font-family:SourceHanSansCN-Regular;
        font-weight:400;
        color:rgba(255,255,255,1);
    }
}
</style>

<template>
    <div class="myProfile">
        <div class="nav_item" style="height: 128rpx;line-height: 128rpx;">
            <span>头像</span>
            <span class="headPortrait" @click="upload">
                <open-data v-if="!dataObj.imgUrl" type="userAvatarUrl"></open-data>
                <img v-if="dataObj.imgUrl" :src="dataObj.imgUrl" alt="">
            </span>
        </div>
        <div class="nav_item">
            <span>昵称</span>
            <input type="text" v-model="dataObj.nickname">
        </div>
        <div class="nav_item" @click="gender_visible = true">
            <span>性别</span>
            <div>{{dataObj.gender}}</div>
            <img class="icon" src="/static/images/ysj.png" alt="">
        </div>
        <div class="nav_item" @click="identity_visible = true">
            <span>身份</span>
            <div>{{dataObj.identity}}</div>
            <img class="icon" src="/static/images/ysj.png" alt="">
        </div>
        <div class="nav_item">
            <span>年龄</span>
            <input type="text" v-model="dataObj.age">
        </div>
        <div class="nav_item">
            <span>身高</span>
            <input type="text" v-model="dataObj.height">
        </div>
        <div class="nav_item" @click="schooling_visible = true">
            <span>学历</span>
            <div>{{dataObj.schooling}}</div>
            <img class="icon" src="/static/images/ysj.png" alt="">
        </div>
        <div class="nav_item">
            <span>邮箱</span>
            <input type="text" v-model="dataObj.email">
        </div>
        <div class="nav_item">
            <span>我的优势</span>
            <input type="text" v-model="dataObj.advantage" style="padding-left:30rpx;">
        </div>
        <div class="nav_item">
            <span>工作描述</span>
            <input type="text" v-model="dataObj.describe" style="padding-left:30rpx;">
        </div>
        <div class="The_divider"></div>
        <div class="formSubmit" @click="formSubmit">保存</div>
        <!-- 性别 -->
        <i-action-sheet :visible="gender_visible" :actions="gender_actions" show-cancel @cancel="genderHandleCancel" @click="genderHandleClickItem" />
        <!-- 身份 -->
        <i-action-sheet :visible="identity_visible" :actions="identity_actions" show-cancel @cancel="identityHandleCancel" @click="identityHandleClickItem" />
        <!-- 身份 -->
        <i-action-sheet :visible="schooling_visible" :actions="schooling_actions" show-cancel @cancel="schoolingHandleCancel" @click="schoolingHandleClickItem" />
    </div>
</template>

<script>
export default {
    data () {
        return {
            dataObj:{
                imgUrl:'',
                nickname:'',
                gender:'',
                identity:'',
                age:'',
                height:'',
                schooling:'',
                email:'',
                advantage:'',
                describe:''
            },
            gender_visible:false,
            gender_actions:[{name: '男'},{name: '女'}],
            identity_visible:false,
            identity_actions:[{name: '在校学生'},{name: '自由工作者'},{name: '兼职人员'}],
            // 学历
            schooling_visible:false,
            schooling_actions:[
                {
                    name: '小学'
                },
                {
                    name: '初中'
                },
                {
                    name: '中专'
                },
                {
                    name: '高中'
                },
                {
                    name: '大专'
                },
                {
                    name: '本科'
                },
                {
                    name: '硕士'
                },
                {
                    name: '博士'
                }
            ]
            
        }
    },
    onLoad() {
        wx.setNavigationBarTitle({
          title:'我的资料',
        })
    },
    mounted () {
        
    },
    methods: {
        upload () {
            var that = this
            wx.chooseImage({
                count: 1,
                sizeType: ['original', 'compressed'],
                sourceType: ['album', 'camera'],
                success(res) {
                    // tempFilePath可以作为img标签的src属性显示图片
                    const tempFilePaths = res.tempFilePaths[0]
                    that.dataObj.imgUrl = tempFilePaths
                }
            })
        },
        formSubmit() {
            console.log(this.dataObj)
        },
        genderHandleCancel () {
            this.gender_visible = false
        },
        genderHandleClickItem (detail) {
            let val = detail.mp._relatedInfo.anchorTargetText
            if (val != '取消' && val != '') {
                this.dataObj.gender = val
                this.gender_visible = false
            }  
        },
        identityHandleCancel () {
            this.identity_visible = false
        },
        identityHandleClickItem (detail) {
            let val = detail.mp._relatedInfo.anchorTargetText
            if (val != '取消' && val != '') {
                this.dataObj.identity = val
                this.identity_visible = false
            }
        },
        schoolingHandleCancel () {
            this.schooling_visible = false
        },
        schoolingHandleClickItem (detail) {
            let val = detail.mp._relatedInfo.anchorTargetText
            if (val != '取消' && val != '') {
                this.dataObj.schooling = val
                this.schooling_visible = false
            }
        },
        
    }
}
</script>
