<template>
  <div class="content">
      <table>
        <thead>
          <tr>
            <td>序号</td>
            <td>标题</td>
            <td>内容</td>
            <td>操作</td>
          </tr>
        </thead>
        <tbody>
          <!-- 调用父组件传递过来的props数据 -->
          <tr v-for="item in dataList" :key="item.id">
            <td>{{item.id}}</td>
            <td>{{item.title}}</td>
            <td>{{item.content}}</td>
            <td>
              <button @click="bianji(item)">编辑</button>
              <button @click="del(item.id)">删除</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
</template>

<script>
import vm from "../utils/vm";
export default {
  props:['dataList'],
  methods:{
    // 编辑
    bianji(item){
      // 通过vm.$emit()触发自定义事件
      vm.$emit('sendData',item);
    },
    del(id){
      this.$emit('delete',id);
    }
  }
}
</script>

<style scoped>
.content {
  margin-top: 20px;
  border: 2px solid blue;
  height: 300px;
}
table {
  width: 600px;
  margin: 0 auto;
}
table,
td {
  border: 1px solid #666;
}
td {
  text-align: center;
}
</style>