<template>
  <div class="retieve">
    <div class="headss">
      <div style="width: 949px;margin: 0 auto;font-size: 18px;line-height: 60px;font-weight: 700;">教师、教育行政干部法治素养提升平台
        <span style="font-size: 17px;color: #333333;font-weight:normal">找回密码</span>
      </div>
    </div>
    <div class="sf">
      <el-steps :active="2" align-center style="width: 670px;margin: 0 auto;">
        <el-step title="身份验证" description=""></el-step>
        <el-step title="设置新密码" description=""></el-step>
        <el-step title="完成" description=""></el-step>
        <!--      <el-step title="步骤4" description="这是一段很长很长很长的描述性文字"></el-step>-->
      </el-steps>
    </div>
    <div class="hm">
<!--      <div style="font-size: 14px;color: #333333;margin-left: 292px;margin-bottom: 26px">请输入重置密码的手机号</div>-->
      <div style="font-size: 14px;color: #333333;margin-left: 292px;margin-bottom: 24px;">
        新密码
        <el-input style="width: 229px;height: 39px;margin-left: 26px;margin-right:10px;" v-model="input" placeholder="请输入新密码" show-password></el-input>
        <span style="color: #999">6~16个字符，区分大小写</span>
      </div>
      <div style="font-size: 14px;color: #333333;margin-left: 278px;margin-bottom: 24px;margin-right:10px;">
        确认密码
        <el-input style="width: 229px;height: 39px;margin-left: 26px" v-model="inputs" placeholder="请再次填写密码" show-password></el-input>
        <span style="color: #999">请再次填写密码</span>
      </div>
      <!-- <div style="text-align:center;font-size: 14px;line-height: 66px">提示:{{ts}}</div> -->
      <el-button type="primary" style="width: 225px;margin:30px auto;display: block" @click="handleNext">下一步</el-button>
    </div>
    <el-main>版权所有 教育部全国青少年普法网   京ICP备10216160号-14</el-main>
  </div>
</template>

<script>
import axios from 'axios'
  import {baseURL} from '@/utils/constant'
import qs from 'qs'
  export default {
    name: 'retieve',
    data(){
      return{
        input:'',
        inputs:'',
        ts:''
      }
    },
    computed: {

    },
    methods: {
      handleNext(){
        let _this = this
        if(_this.input !== _this.inputs){
          _this.$message({
            message: '两次填写的密码不一致,请重新输入',
            type: 'warning'
          })
        }else if(_this.input == ''){
          _this.$message({
            message: '密码不能为空,请输入密码',
            type: 'warning'
          })
        }else{
          axios.post(baseURL + '/login/resetPassword', qs.stringify({
              mobile: _this.$route.query.mobile,
              password: _this.inputs
            }))
          .then(function (response) {
            if(response.data.status === '0'){
              _this.$router.push({path:'/complete'})
            }else{
              _this.$message({
                message: response.data.message,
                type: 'warning'
              })
            }
          })
          .catch(function (error) {
            console.log(error)
          })
        }
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
