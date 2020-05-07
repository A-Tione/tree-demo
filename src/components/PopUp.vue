<template>
  <div class="pop-up-content">
    <div class="app-box" v-for="(item,index) in list" :key="index">
      <img class="img" :src="item.img">
      <p class="text">{{item.name}}</p>
    </div>
  </div>
</template>

<script>
  export default {
    name: "PopUp",
    props: {
      list: {
        type: Array,
        default: ()=> []
      }
    },
    data() {
      return {}
    },

    mounted() {
    },
    methods: {}

  }
</script>

<style lang="scss" scoped>
  .pop-up-content {
    position: relative;
    box-sizing: border-box;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    width: 514px;
    max-height: 248px;
    background: white;
    border-radius: 6px;
    box-shadow: 0 1px 12px 0 rgba(107, 118, 156, 0.2);
    .app-box {
      width: 124px;
      height: 124px;
      padding: 8px;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      .img {
        width: 40px;
        height: 40px;
        margin-bottom: 8px;
      }
      .text {
        font-size: 12px;

      }
    }
  }

</style>