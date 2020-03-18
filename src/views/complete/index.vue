<template>
  <div class="retieve">
    <div class="headss">
      <div style="width: 949px;margin: 0 auto;font-size: 18px;line-height: 60px;font-weight: 700;">教师、教育行政干部法治素养提升平台
        <span style="font-size: 17px;color: #333333;font-weight:normal">找回密码</span>
      </div>
    </div>
    <div class="sf">
      <el-steps :active="3" align-center style="width: 670px;margin: 0 auto;">
        <el-step title="身份验证" description=""></el-step>
        <el-step title="设置新密码" description=""></el-step>
        <el-step title="完成" description=""></el-step>
        <!--      <el-step title="步骤4" description="这是一段很长很长很长的描述性文字"></el-step>-->
      </el-steps>
    </div>
    <div class="hm">
      <div style="line-height: 232px;text-align: center;">密码重置成功</div>
      <el-button type="primary" style="width: 225px;margin:0 auto;display: block" @click="handleLogin">登录</el-button>
    </div>
    <el-main>版权所有 教育部全国青少年普法网   京ICP备10216160号-14</el-main>
  </div>
</template>

<script>

  export default {
    name: 'retieve',
    data(){
      return{
        input:'',
        yzm:'',
        ts:''
      }
    },
    computed: {

    },
    methods: {
      handleLogin(){
        this.$router.push({ path: '/login' })
      }
    }
  }
</script>

<style lang="scss" scoped>
  .retieve{
    width: 100%;
    overflow: hidden;
  }
  .headss{
    width: 100%;
    height: 60px;
    border-bottom: 1px solid rgba(204, 204, 204, 1);;
  }
  .sf{
    width: 949px;
    height:85px;
    background: rgba(242, 242, 242, 1);
    margin: 0 auto;
    margin-top: 100px;
    padding-top: 20px;
  }
  .hm{
    width: 949px;
    background:rgba(255, 255, 255, 1);
    height: 383px;
    border: 1px solid rgba(255, 255, 255, 1);
    margin: 0 auto;
    box-shadow: 0px 0px 6px rgba(51, 51, 51, 0.349019607843137);
    padding-top: 50px;
    border-bottom: 1px solid #ccc;
  }
  .el-main {
    color: #333;
    text-align: center;
    line-height: 50px;
    margin-top: 270px;
    font-size: 12px;
    color: #999999;
  }
</style>
