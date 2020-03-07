<template>
    <div>
        <wbc-nav></wbc-nav>
        <div class="container">
            <el-row  :gutter="30">
                <el-col :sm="24" :md="16" style="transition:all .5s ease-out;margin-bottom:30px;">
                    <el-input v-model="title" placeholder="文章标题"></el-input>
                    <el-select v-model="tagId" @change="handleChange">
                      <el-option v-for="item in selectList" :key="item.whsCode" :label="item.id" :value="item.value"></el-option>
                    </el-select>
                    <Ueditor :value="ueditor.value" :config="ueditor.config" ref="ue"></Ueditor>        
                    <h1 class="tcolors-bg" @click="returnContent">提交</h1>
                </el-col>
                <el-col :sm="24"  :md="8" >
                    <wbc-rightlist></wbc-rightlist>
                </el-col>
            </el-row>
        </div>
        <wbc-footer></wbc-footer>
    </div>

</template>

<script>
import header from '../components/header.vue'
import footer from '../components/footer.vue'
import temRightlist from '../components/temRightlist.vue'
import Ueditor from "../components/ueditor";
import {
	addBlog
} from '../utils/server.js'
export default {
  data() {
    return {
      title: '',
      sendTip:'发送~',
      dat: {
        content: "",
      },
      ueditor: {
        value: "慢慢写~",
        config: {}
      },
      tagId:'',
      selectList:[
        {id:'技术积累',value: 1},
        {id:'读书笔记',value: 2},
        {id:'读paper笔记',value: 3},
        {id:'心境',value: 4},
        {id:'其他',value: 5}
      ]
    };
  },
  methods: {
    handleChange(val){
      var obj = {}
      obj = this.selectList.find(function(item){
        return item.value === val
      })
    },
    returnContent() {
      this.dat.content = this.$refs.ue.getUEContent();
      console.log(this.title);
      console.log(this.dat.content);
      console.log(this.tagId);
      let data = {"title":this.title, "content":this.dat.content, "classId":this.tagId};
      addBlog(data, function(msg) {

      })
    },
    showContent() {
      this.show = !this.show;
    }
  },
  components: {
    'wbc-nav':header,
    'wbc-footer':footer,
    'wbc-rightlist':temRightlist,
    Ueditor
  },
};
</script>

<style>

.container h1 {
    /*background: #97dffd;*/
    color:#fff;
    border-radius: 5px;
    cursor: pointer;
    /*transition: all .3s ease-in-out;*/
    height:30px;
    line-height: 30px;
    text-align: center;
}
</style>