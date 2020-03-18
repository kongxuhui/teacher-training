<template>
  <div class="retieve">
    <div class="headss">
      <div style="width: 949px;margin: 0 auto;font-size: 18px;line-height: 60px;font-weight: 700;">教师、教育行政干部法治素养提升平台
        <span style="font-size: 17px;color: #333333;font-weight:normal">找回密码</span>
      </div>
    </div>
    <div class="sf">
      <el-steps :active="1" align-center style="width: 670px;margin: 0 auto;">
        <el-step title="身份验证" description=""></el-step>
        <el-step title="设置新密码" description=""></el-step>
        <el-step title="完成" description=""></el-step>
        <!--      <el-step title="步骤4" description="这是一段很长很长很长的描述性文字"></el-step>-->
      </el-steps>
    </div>
    <div class="hm">
      <div style="font-size: 14px;color: #333333;margin-left: 292px;margin-bottom: 26px">请输入重置密码的手机号</div>
      <div style="font-size: 14px;color: #333333;margin-left: 292px;margin-bottom: 24px">
        手机号
        <el-input style="width: 250px;height: 39px;margin-left: 26px" v-model="input" placeholder="请输入手机号"></el-input>
      </div>
      <div style="font-size: 14px;color: #333333;margin-left: 292px;">
        验证码
        <el-input style="width: 120px;height: 39px;margin-left: 26px" v-model="yzm" placeholder="请输入验证码"></el-input>
        <el-button v-show="show" style="margin-left: 14px;width: 112px;" @click="getCode">{{title}}</el-button>
        <el-button v-show="!show" style="margin-left: 14px;width: 112px;" @click="getCode" disabled="">重新发送({{count}}s)</el-button>
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
    name: 'retrieve',
    data(){
      return{
        input:'',
        yzm:'',
        ts:'',
        title: '发送验证码',
        show: true,
        count: '',
        timer: null,
      }
    },
    computed: {

    },
    methods: {
      handleNext(){
        let _this = this
        axios.get(baseURL + '/SMS/verifySMSCode', {
          params: {
            mobile: _this.input,
            code: _this.yzm
          }
        })
        .then(function (response) { 
          if(response.data.status === '0'){
            _this.$router.push({path:'/password?mobile=' + _this.input})
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
      },
      getCode(){
        let _this = this
        const partten = /^(13[0-9]|14[0-9]|15[0-9]|16[6]|18[0-9]|19[6,9]|17[0-9])\d{8}$/i
        if(partten.test(_this.input)){
          const TIME_COUNT = 30
          if (!_this.timer) {
           _this.count = TIME_COUNT
           _this.show = false
           _this.timer = setInterval(() => {
           if (_this.count > 0 && _this.count <= TIME_COUNT) {
             _this.count--
            } else {
             _this.show = true
             clearInterval(_this.timer);
             _this.timer = null
              _this.title = '重新发送'
            }
           }, 1000)
          }
          axios.post(baseURL + '/SMS/sendSMSCode', qs.stringify({
              mobile: _this.input
            }))
          .then(function (response) { 
            if(response.data.status === '0'){
              _this.$message({
                message: '验证码发送成功',
                type: 'success'
              })
            }
          })
          .catch(function (error) {
            console.log(error)
          })
        }else{
          _this.$message.error('您输入的手机号码格式有误，请重新输入.')
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
  .el-step__icon.is-text {
      border-radius: 50%;
      background-color: #008EFF!important;
      /* border: 2px solid; */
      color: #fff;
      border-color: inherit;
  }
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
