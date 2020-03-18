<template>
  <div class="dashboard-container">
    <div style="border-bottom: 1px solid #ccc;overflow:hidden;">
      <div class="dashboard-text">宪法与国家</div>
    </div>
    <div class="cyt">
      <div class="cytss">
        <div class="cytss_t"></div>
        <div class="cytss_b">
          第一章   宪法：国家的根本法
          <div></div>
        </div>
      </div>
      <div class="cytss">
        <div class="cytss_t"></div>
        <div class="cytss_b">
          第二章   维护国家荣誉
        </div>
      </div>
      <div class="cytss">
        <div class="cytss_t"></div>
        <div class="cytss_b">
          第三章   国家安全犯罪
        </div>
      </div>

    </div>
    <div class="cyt">
      <div class="cytss">
        <div class="cytss_t"></div>
        <div class="cytss_b">
          第四章   海洋法知识（南海主权）
        </div>
      </div>
      <div class="cytss" style="visibility:hidden;">

      </div>
      <div class="cytss" style="visibility:hidden;">

      </div>
    </div>
  </div>
</template>


<script>
  import { mapGetters } from 'vuex'

  export default {
    name: 'Dashboard',
    data(){
      return {
        input:'',
        inputs:''
      }
    },

    computed: {
      ...mapGetters([
        'name'
      ])
    }
  }

</script>

<style lang="scss" scoped>
  .dashboard {
    &-container {
      margin: 30px;
    }
    &-text {
      font-size: 30px;
      line-height: 46px;
    }
  }
  .dashboard-text{
    width: 6%;
    border-bottom: 1px solid #000;
    font-size: 14px;
  }
  .cyt{
    height: 224px;
    display: flex;
    justify-content: space-around;
    margin-top: 40px;
  }
  .cytss{
    width: 198px;
    height: 224px;
    border: 1px solid #ccc;
    overflow: hidden;
  }
  .cytss_t{
    width: 100%;
    height: 138px;
  }
  .cytss_b{
    width: 100%;
    height: 87px;
    text-align: center;
    font-size: 13px;
  }
</style>
