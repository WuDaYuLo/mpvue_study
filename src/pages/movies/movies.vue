<template>
    <div>
        <div @tap="toMoviesDetail(index)" v-for="(item , index) in moviesArr" class="moviesContainer" :key="index">
        <img class="movies_img" :src="item.images.large" alt="">
        <div class="movies_info">
            <p class="movies_name">{{item.original_title}}</p>
            <p class="movies_year">年份：{{item.year}}</p>
            <p class="movies_dir">导演：{{item.directors[0].name}}</p>
        </div>
        <p class="movies_rating">{{item.rating.average}}</p>
    </div>
    </div>
</template>


<script>

// 豆瓣的地址
const MOVIE_URL = 'http://t.yushu.im/v2/movie/top250';

export default {
    data(){
        return{
            moviesArr:[]
        }
    },
    beforeMount() {
        //axios   小程序不能用axios 会报错： XMLHttpRequest is not a constructor
        // fly.js  https://github.com/wendux/fly 代替
        this.$fly.get(MOVIE_URL)
            .then( (response)=> {
                console.log(response);
                let moviesArr = response.data.subjects
                this.moviesArr = moviesArr 
            
                this.$store.dispatch("getmoviesArr",moviesArr)
      
            })
            .catch( (error)=> {
                console.log(error);
            });
    },

     methods: {
         toMoviesDetail(index){
             wx.navigateTo({
                 url: '/pages/moviesDetail/main?index=' + index,
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
     },
}
</script>


<style>
    .moviesContainer{
        display: flex;
        padding: 10rpx;
        border-bottom: 1rpx solid #eee;
    }
    .moviesContainer .movies_img{
        width: 128rpx;
        height: 128rpx;
        margin-right:20rpx;
    }
    .movies_info{
        width: 70%;

    }
    .movies_name{
        font-size: 32rpx;
        color: #333;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }
    .movies_year{
        font-size:28rpx;
        color: #999;
        margin: 6rpx 0;
    }
    .movies_dir{
        font-size: 30rpx;
        color: #666;
    }
    
    .movies_rating{
        font-size: 36rpx;
        font-weight: bold;
        color: #f00;
    }
    
</style>