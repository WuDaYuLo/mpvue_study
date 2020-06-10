<template>
    <div @tap="toDetail" class="tmpContainer">
        <div class="avatar_date">
            <img :src="item.avatar" alt="">
            <span>{{item.date}}</span>
        </div>
        <p class="company">{{item.title}}</p>
        <img class="detail_img" :src="item.detail_img" alt="">
        <p class="content">{{item.detail_content}}</p>
        <div class="view_start_container">
            <img src="/static/images/icon/star.png" alt="">
            <span>{{item.love_count}}</span>
            <img src="/static/images/icon/view.png" alt="">
            <span>{{item.attention_count}}</span>
        </div>
    </div>
</template>

<script>
export default {
    props:[
         'item', 'index'
    ],
    methods: {
        toDetail(){
            // 跳转到详情页 + 传参过去index
            wx.navigateTo({
                url: '/pages/detail/main?index='+this.index
            })
        }
    },
}
</script>


<style>
    .tmpContainer{
        display: flex;
        flex-direction: column;
        border-bottom: 1rpx solid #ccc;

    }

    .avatar_date img{
        width: 60rpx;
        height: 60rpx;
        border-radius: 50%;
        vertical-align: middle;
        margin-right: 10rpx;
    }

    .avatar_date {
        padding: 10rpx;
    }

    .avatar_date span{
        font-size: 28rpx;
        color: #333;
    }
    .company{
        font-size: 40rpx;
        font-weight: bold;
        padding: 10rpx;
    }

    .detail_img{
        width: 100%;
        height: 400rpx;

    }

    .content{
        font-size: 32rpx;
        text-indent: 32rpx;
        line-height: 50rpx;
        letter-spacing: 3rpx;
        /* word-spacing  针对的是英文单词 */
        /* letter-spacing  针对的是字母和中文 */
    }

    .view_start_container img{
        width: 32rpx;
        height: 32rpx;
        vertical-align: middle;
        margin-left: 10rpx;
    }

    .view_start_container span{
        font-size: 28rpx;
        color: #333;
        margin-left: 10rpx;

    }
</style>