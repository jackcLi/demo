<template>
  <div class="home">
    <van-nav-bar title="首页" left-arrow @click-left="$router.back()" />
    <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
      <van-swipe-item v-for="item in banners" :key="item">
        <img :src="item" alt="" />
      </van-swipe-item>
    </van-swipe>
    <van-grid :column-num="3">
      <van-grid-item
        v-for="value in categories"
        :key="value._id"
        :icon="value.coverImg"
        :text="value.name"
        :to="{ name: 'Hot', query: { c: value._id } }"
      />
    </van-grid>
    
    
  </div>
</template>

<script>
// @ is an alias to /src
// import引入一个文件
import { allCategories } from "@/services/categories";
// import qz from "../assets/qz.png";

export default {
  name: "Home",
  data() {
    return {
      // qz, // qz: qz
      banners: [
        "https://s11.mogucdn.com/mlcdn/c45406/201030_351kf5d6bfg5djha481lkdahgl6cl_1060x367.jpg_750x9999.v1c7E.81.webp",
        "https://s17.mogucdn.com/mlcdn/c45406/201030_8095gbl6ch5icek4f6iig49fj6k9c_1060x367.jpg_750x9999.v1c7E.81.webp",
      ],
      categories: [], // 商品分类
    };
  },
  async created() {
    const res = await allCategories();
    this.categories = res.categories;
  },
  components: {},
};
</script>
<style scoped>
.my-swipe .van-swipe-item img {
  width: 100%;
}
</style>
