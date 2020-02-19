<template>
    <div>
        <wbc-nav></wbc-nav>
        <div class="container">
            <el-row  :gutter="30">
                <el-col :sm="24" :md="16" style="transition:all .5s ease-out;margin-bottom:30px;">
                    <Ueditor :value="ueditor.value" :config="ueditor.config" ref="ue"></Ueditor>
                    <input type="button" value="显示编辑器内容（从控制台查看）" @click="returnContent">
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
export default {
  data() {
    return {
      sendTip:'发送~',
      dat: {
        content: "",
      },
      ueditor: {
        value: "编辑默认文字",
        config: {}
      }
    };
  },
  methods: {
    returnContent() {
      this.dat.content = this.$refs.ue.getUEContent();
      console.log(this.dat.content);
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
  }
};
</script>