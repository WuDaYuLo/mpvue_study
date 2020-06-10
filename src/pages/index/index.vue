<template>
    <div class="indexContainer">
        <img v-if="isShow" class="index_img" :src="userInfo.avatarUrl" alt="">
        <button class="btn" v-else open-type="getUserInfo" @getuserinfo="getUserInfo">点击获取用户的信息</button>
        <p class="username">hello {{userInfo.nickName}}</p>
        <div @tap="toDetail" class="goStudy">
            <span>开启小程序之旅</span>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return {
            userInfo: { },
            isShow:false //用户没有授权
        }
    },
    
    beforeMount(){
        console.log("---beforeMount--");
        // 获取用户的信息
        this.handleGetUserInfo();
    },
    methods:{
        // 获取用户登录信息
        handleGetUserInfo(){
            wx.getUserInfo({
                success: (res)=>{
                    // success
                    console.log(res.userInfo);
                    // 跟新data数据
                    // this.userInfo = res.userInfo;
                    this.userInfo = res.userInfo;
                    this.isShow = true;
                },
                fail: ()=> {
                    // fail
                    console.log("获取失败");
                },
                complete: ()=> {
                    // complete
                    // console.log("获取完成");
                }   
            })
        },
        getUserInfo(data){
            // console.log(data);
            // 判断用户是否授权
            if(data.mp.detail.rawData){
                // true 用户授权了
                this.handleGetUserInfo();
            }
        },
        toDetail(){
            // console.log("toDetail");
            wx.switchTab({
                url: '/pages/list/main',
                success: function(res){
                    // success
                },
                fail: function() {
                    // fail
                },
                complete: function() {
                    // complete
                }
            })
        }
    }
}
</script>

<style>
    page{
        background: #8ed145;
    }
    .indexContainer{
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .index_img{
        width: 200rpx;
        height: 200rpx;
        border-radius: 50%;
        margin: 100rpx 0 ;
    }

    .username{
        font-size: 40rpx;
        font-weight: bold;
        margin: 100rpx 0;
    }
    
    .goStudy{
        width: 220rpx;
        height: 80rpx;
        border: 1px solid #eee;
        font-size: 24rpx;
        line-height:80rpx;
        text-align: center;
        border-radius: 10rpx;
    }

    .btn{
        width: 300rpx;
        height: 300rpx;
        line-height: 300rpx;
        text-align:center;
        border-radius: 150rpx;
        margin:100rpx 0;
        font-size: 26rpx;
    }
</style>