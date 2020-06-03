<template>
    <div id="home">
        <nav-bar class="home-nav"><div slot="center">购物车</div></nav-bar>
        <home-swiper :banners="banners"></home-swiper>
        <recommend-view :recommends="recommends"/>
    </div>
</template>

<script>
import NavBar from '@/components/common/navbar/NavBar'
import HomeSwiper from './childComps/HomeSwiper'
import {getHomeMultidata} from '@/network/home'
import RecommendView from './childComps/RecommendView'

export default {
    name:'Home',
    components:{
        NavBar,
        HomeSwiper,
        RecommendView
    },
    data(){
        return{
            result:null,
            banners:[],
            recommends:[]
        }
    },
    created(){
        getHomeMultidata().then(res=>{
            this.result=res;
            console.log(res.data.data.banner.list)
            console.log(res.data.data.recommend.list)
            this.banners=res.data.data.banner.list;
            this.recommends=res.data.data.recommend.list;
        })
    }
}
</script>
<style>
 .home-nav{
     background-color: var(--color-tint);
     color: #fff;
 }
</style>