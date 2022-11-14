<template>
  <div class="container">
    <div class="header">
      <div>
        <input type="text" placeholder="搜索关键词">
        <button>搜索</button>
      </div>
      <button @click="info.isShow=!info.isShow">添加</button>
    </div>
    <List :dataList="dataList" @delete="del"/>
    <Alert :info="info"  @add="addHandle" @update="update" :isAdd.sync='isAdd'/>
  </div>
</template>

<script>
import List from '@/components/List';
import Alert from '../components/Alert.vue';

export default {
  name: 'Home',
  // 注册私有组件
  components: {
    List,
    Alert,
    
  },
  data(){
    return{
      dataList: [
      {
        id: 3,
        title: "标题3",
        content: "内容3"
      },
      {
        id: 2,
        title: "标题2",
        content: "内容2"
      },
      {
        id: 1,
        title: "标题1",
        content: "内容1"
      }
    ],
      info:{isShow:false},
      isAdd:true
    }
  },
  methods: {
    del(id){
      const index = this.dataList.findIndex(item => item.id === id);
      this.dataList.splice(index, 1);
    },
    addHandle (data) {
      console.log(data)
      this.dataList.unshift({
        id: this.dataList.length + 1,
        title: data.title,
        content: data.content
      })
    },
    update(data){
      // console.log(data)
      // this.info.isShow=true
      const index = this.dataList.findIndex(item => item.id === data.id);
      console.log(this.dataList)
      console.log(index)
      if(index < 0){
        return 
      }
      this.dataList[index].title = data.title;
      this.dataList[index].content = data.content;
    }
  },
  watch:{
    'info.isShow':{
      handler:function(nv){
        if(nv){
          this.isAdd = true
        }
      }
    }
  }
}
</script>
<style scoped>
.container {
  padding: 10px;
  background: #eee;
  position: relative;
  height: 100%;
}
.header {
  display: flex;
  justify-content: space-between;
}
</style>
