<template>
  <div class="dashboard-container">
    <div class="min_title">
      <img src="@/assets/image/wanch.png" alt="">
      <span>{{title}} &nbsp; </span>
      <span>&nbsp;&nbsp;  |  &nbsp;&nbsp;&nbsp;&nbsp;{{content}}</span>
    </div>
    <div class="cyt" v-if="!learn">
      <div class="dashboard-text">知识点</div>
        <div class="dv" v-for="(item,idx) in list" :key='idx'> 
          <p> {{item.title}} </p>
          <el-button type="primary" plain @click="handleLearn(item.id)">开始学习</el-button>
          <div class="clear"></div>
        </div>
    </div>
    <div v-else class="cyt">
        <div class="dashboard-text">{{title_1}}<el-button class="learnNext" type="primary" @click="handleLearnNext">下一知识点</el-button></div>
        <div v-html="content_1" class="coon"> {{content_1}} </div>
        <!-- <div class="btn">
          <el-button type="primary" @click="handleLearnNext">学习下一知识点</el-button>
          <el-button type="primary" @click="handleTotop">置顶</el-button>
        </div> -->
    </div>
  </div>
</template>


<script>
  import { mapGetters } from 'vuex'
  import axios from 'axios'
  import {baseURL} from '@/utils/constant'

  export default {
    name: 'Dashboard',
    data(){
      return {
        input:'',
        inputs:'',
        learn: false,
        content: '',
        content_1: '',
        title: '',
        title_1: '',
        currentChapterId: '',
        current_id: '',
        list:[]
      }
    },

    computed: {
      ...mapGetters([
        'name'
      ])
    },
    watch: {
      sessionStorage(val) {
        let _this = this
        axios.get(baseURL + '/content/getContentList/', {
          params: {
            chapterId: sessionStorage.getItem('chapterId'),
            columnId: sessionStorage.getItem('columnId')
          }
        })
        .then(function (response) {
          _this.$data.currentChapterId = sessionStorage.getItem('chapterId')
          _this.$data.list = response.data.data.contentList
        })
        .catch(function (error) {
          console.log(error)
        })
      }
    },
    methods:{
      handleLearn(id){
        this.$data.learn = true
        this.$data.current_id = id
        let _this = this
        axios.get(baseURL + '/content/getContent', {
          params: {
            contentId: this.$data.current_id
          }
        })
        .then(function (response) {
          _this.content_1 = response.data.data.content.content
          _this.title_1 = response.data.data.content.title
        })
        .catch(function (error) {
          console.log(error)
        })
      },
      handleLearnNext(){
        this.$data.current_id = Number(this.$data.current_id) + 1
        let _this = this
        axios.get(baseURL + '/content/getContent', {
          params: {
            contentId: this.$data.current_id
          }
        })
        .then(function (response) {
          _this.content_1 = response.data.data.content.content
          _this.title_1 = response.data.data.content.title
        })
        .catch(function (error) {
          console.log(error)
        })
      },
      handleTotop(){

      }
    },
    created(){
      let _this = this
      if(_this.$data.currentChapterId != sessionStorage.getItem('chapterId')){
        axios.get(baseURL + '/content/getContentList/', {
          params: {
            chapterId: sessionStorage.getItem('chapterId'),
            columnId: sessionStorage.getItem('columnId')
          }
        })
        .then(function (response) {
          _this.$data.currentChapterId = sessionStorage.getItem('chapterId')
          _this.list = response.data.data.contentList
          _this.title = sessionStorage.getItem('title')
          _this.content = response.data.data.chapterName
          sessionStorage.setItem('content', _this.content)
        })
        .catch(function (error) {
          console.log(error)
        })
      }else{
        _this.title = sessionStorage.getItem('title')
        _this.content = sessionStorage.getItem('content')
        axios.get(baseURL + '/content/getContentList/', {
          params: {
            chapterId: sessionStorage.getItem('chapterId'),
            columnId: sessionStorage.getItem('columnId')
          }
        })
        .then(function (response) {
          _this.$data.currentChapterId = sessionStorage.getItem('chapterId')
          _this.list = response.data.data.contentList
        })
        .catch(function (error) {
          console.log(error)
        })
      }
    }
  }

</script>

<style lang="scss" scoped>
.learnNext{
  float: right;
  margin-right: 20px;

}
  .min_title{
    width: 100%;
    height: 50px;
    line-height: 50px;
    padding: 0 0 0 30px;
    color: #000000;
    background:rgba(255,255,255,1);
    border:1px solid rgba(51,165,255,1);
    border-radius:5px;
    font-weight:400;
    img{
      width: 24px;
      vertical-align: middle;
      margin-right: 16px;
    }
  }
  .coon{
    height: calc(100vh - 380px);
    overflow-x: hidden;
    overflow-y: auto;
  }
  .coon::-webkit-scrollbar {
      width: 2px;    
      /*height: 4px;*/
  }
  .coon::-webkit-scrollbar-thumb {
      border-radius: 10px;
      -webkit-box-shadow: inset 0 0 5px rgba(0,0,0,0.2);
      background: rgba(0,0,0,0.2);
  }
  .coon::-webkit-scrollbar-track {
      -webkit-box-shadow: inset 0 0 5px rgba(0,0,0,0.2);
      border-radius: 0;
      background: rgba(0,0,0,0.1);

  }
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
    font-size:16px;
    font-family:'PingFangSC-';
    font-weight:400;
    color:rgba(0,0,0,1);
    padding-left: 20px;
  }
  .cyt{
    padding: 20px 10px;
    background:rgba(255,255,255,1);
    border:1px solid rgba(51,165,255,1);
    border-radius:5px;
    margin-top: 20px;
    .btn{
      text-align: center; 
      position: fixed;  
      bottom: 20px; 
      border-bottom: 0px solid #eee;
      .el-button{
        float: none;
      }
    }
    .dv{
      width: 96%;
      background:rgba(255,255,255,1);
      box-shadow:0px 0px 10px 0px rgba(19,36,50,0.2);
      border-radius:5px;
      border-bottom: 1px solid #eee;
      margin: 8px auto;
      height:50px;
      p{
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-line-clamp: 1;
        line-height: 50px;
        float: left;
        font-size: 14px;
        color: #000;
        width: 80%;
        -webkit-box-orient: vertical;
        margin: 0;
        padding: 0 20px;
      }
      .el-button{
        float: right;
        background:rgba(255,109,51,1);
        border-radius:4px;
        margin-right: 20px;
        margin-top: 6px;
        font-size:10px;
        font-family:'PingFangSC-';
        font-weight:400;
        color:rgba(255,255,255,1)
      }
      .clear{
        border: 0px solid #000;
        clear: both;
      }
    }
  }
</style>
