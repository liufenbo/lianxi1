<template>
  <div class="alert" v-show="info.isShow">
    <h3>添加</h3>
    <div>
      标题:
      <input type="text" placeholder="请输入标题"  v-model.trim="formData.title"/>
    </div>
    <div>
      内容:
      <input type="text" placeholder="请输入内容"  v-model.trim="formData.content"/>
    </div>
    <div class="options">
      <button @click="submit">提交</button>
      <button @click="cancel">取消</button>
    </div>
  </div>
</template>

<script>
import vm from "../utils/vm";
export default {
  mounted() {
    vm.$on("sendData", data => {
      this.info.isShow = true;
      this.$nextTick(()=>{
        this.$emit('update:isAdd',false)
      })
      this.formData = { ...data };
      this.current = { ...data };
    });
  },
  methods:{
    // 提交
    submit(){
      if (this.formData.title === "") {
        return alert("请输入标题");
      }
      if (this.formData.content === "") {
        return alert("请输入内容");
      }
      console.log(this.isAdd)
      if (!this.isAdd) {
        // 更新
        this.update();
      } else {
        // 新增
        this.$emit("add", this.formData);
      }
      this.reset();
      this.cancel();
    },
    //取消
    cancel(){
      this.info.isShow=false;
      this.reset();
    },
    //重置
    reset(){
      this.formData={
        title:"",
        content:""
      };
    },
    //更新
    update(){
      this.$emit("update", this.formData);
      console.log(this.current);
    }
  },
  props:['info','isAdd'],//使用属性名接收
  data(){
    return{
      formData:{
        title:"",
        content:""
      },
      current:{}
    }
  }
}
</script>

<style scoped>
.alert {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: #fff;
  width: 400px;
  height: 300px;
}
.alert h3 {
  background: blue;
  color: #fff;
  height: 40px;
  line-height: 40px;
  padding-left: 10px;
}
.alert .options {
  position: absolute;
  bottom: 0px;
  left: 0;
  padding: 10px;
  background: #ddd;
  width: 100%;
  text-align: center;
}
</style>