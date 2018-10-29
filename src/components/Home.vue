<template>
    <div class="home">
        <scroll-img :img-list="imgList"></scroll-img>
    </div>
</template>
<script>
import ScrollImg from "../components/ScrollImage.vue";
export default {
  components: {
    "scroll-img": ScrollImg
  },
  data() {
    return {
      imgList: [
        {
          img:
            "https://img.alicdn.com/tfs/TB1zu9diYPpK1RjSZFFXXa5PpXa-520-280.jpg"
        },
        {
          img:
            "https://aecpm.alicdn.com/simba/img/TB1JNHwKFXXXXafXVXXSutbFXXX.jpg"
        },
        {
          img: "https://img.alicdn.com/tps/i4/TB1umHqi4TpK1RjSZFMwu2G_VXa.png"
        },
        {
          img:
            "https://img.alicdn.com/simba/img/TB1WomizkOWBuNjSsppSutPgpXa.jpg"
        },
        {
          img:
            "https://aecpm.alicdn.com/simba/img/TB183NQapLM8KJjSZFBSutJHVXa.jpg"
        }
      ]
    };
  }
};
</script>

<style scoped>

.home{
    width: 500px;
    height: 300px;
}

</style>
