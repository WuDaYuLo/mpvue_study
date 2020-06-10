<template>
    <div>
        <div class="moviesDetailContainer" v-if="moviesDetail.images">
            <img :src="moviesDetail.images.large" alt="">
            <p class="movie_name">{{moviesDetail.original_title}}</p>
            <div class="detail_content">
                <span>评分：{{moviesDetail.rating.average}}</span>
                <span>导演：{{moviesDetail.directors[0].name}}</span>
                <span>主演：{{moviesDetail.casts[0].name}} {{moviesDetail.casts[1].name}} {{moviesDetail.casts[2].name}}</span>
            </div>
            <button>我要观影</button>
        </div>        
    </div>
</template>

<script>
import {mapState} from 'vuex'
export default {
    data() {
        return {
            moviesDetail:{}
        }
    },
    computed: {
        ...mapState(['moviesArr'])
    },

    beforeMount() {
        console.log(this)
        // this.index = this.$mp.query.index
        this.moviesDetail = this.moviesArr[this.$mp.query.index]
        console.log(this.moviesDetail)
    },
}
</script>

<style>
    .moviesDetailContainer{
        display: flex;
        flex-direction: column;
        /* align-items: center; */
    }

    .moviesDetailContainer img{
        width: 70%;
        height: 700rpx;
        margin: 50rpx auto;
    }

    .movie_name{
        font-size: 40rpx;
        font-weight: bold;
        text-align: center;
    }

    .detail_content{
        display: flex;
        flex-direction: column;
        margin-left: 20%;
        margin-top: 30rpx;
        line-height: 50rpx;
        font-size: 26rpx;

    }

    button{
        width: 70%;
        height: 80rpx;
        background-color: green;
        line-height: 80rpx;
        color: #fff;
        margin-top: 28rpx;
        font-size: 28rpx;
        
    }

</style>