<template>
  <div class="box">
    <el-row>
      <el-button type="primary" round @click="add">添加</el-button>
      <v-list @edit="edit"></v-list>
      <v-add :info="info" ref="add"></v-add>
    </el-row>
  </div>
</template>
<script>
import vAdd from "./component/add";
import vList from "./component/list";
export default {
  components: {
    vAdd,
    vList,
  },
  data() {
    return {
      info:{
        show:false,
        isAdd:false,
        title:'商品分类'
      }
    };
  },
  methods: {
    // 点了seckill添加
    add() {
        this.info.show=true,
        this.info.isAdd=true,
        this.info.title='秒杀添加'
        // this.$refs.add.getDetail(id)
    },
    // 点了编辑
    edit(id){
        this.info.show=true,
        this.info.isAdd=false,
        this.info.title='秒杀修改'
        this.$refs.add.getDetail(id)
    }
  },
  mounted() {
  },
};
</script>
<style scope>
.box {
  padding-top: 20px;
}
</style>