<template>
  <div class="pop-up-content">
    <div class="app-box" v-for="(item,index) in list" :key="index">
      <div class="box">
        <img class="img" :src="item.img">
        <p class="text">{{item.name}}</p>
      </div>
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
    overflow: auto;
    &::before,.box:after{
      position:absolute;
      content:'';
      left:65%;
      overflow:hidden;
      pointer-events:none;
      -webkit-transform:rotate(45deg);
      -mz-transform:rotate(45deg);
      transform:rotate(45deg);
    }
    &::before{
      box-shadow:0px 0px 6px #ccc;
      top:-7px;
      width:14px;
      height:14px;
      margin-left:-7px;
    }
    &::after{
      top:-6px;
      width:18px;
      height:18px;
      margin-left:-9px;
      background:#fff;
      box-shadow:none;
    }
    .app-box {
      position: relative;
      width: 124px;
      height: 124px;
      padding: 8px;
      &::after {
        position: absolute;
        top: 25px;
        right: 100%;
        content: '';
        width: 1px;
        height: 72px;
        background: #E9EAEC;
      }
      .box {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        cursor: pointer;
        width: 100%;
        height: 100%;
        &:hover {
          background: #EBF7FF;
        }
        .img {
          width: 40px;
          height: 40px;
          margin-bottom: 14px;
        }
        .text {
          width: 100%;
          overflow: hidden;
          white-space: nowrap;
          text-overflow: ellipsis;
          font-size: 12px;
          text-align: center;
        }
      }
    }
  }

</style>