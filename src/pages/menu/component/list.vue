<template>
  <div class="box">
    <!-- list列表渲染 -->

    <el-table
      :data="menuList"
      style="width: 100%;margin-bottom: 20px;"
      row-key="id"
      border
      :tree-props="{children: 'children', hasChildren: 'hasChildren'}"
    >
      <el-table-column prop="id" label="菜单编号" sortable width="180"></el-table-column>

      <el-table-column prop="title" label="菜单名称" sortable width="180"></el-table-column>

      <el-table-column label="菜单图标">
        <template slot-scope="scope">
          <i :class="scope.row.icon"></i>
        </template>
      </el-table-column>

   <el-table-column prop="url" label="菜单地址"></el-table-column>

      <el-table-column label="状态">
        <template slot-scope="scope">
          <el-button type="primary" v-if="scope.row.status==1">启用</el-button>
          <el-button type="info" v-else>禁用</el-button>
        </template>
      </el-table-column>

      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button type="primary" @click="edit(scope.row.id)">编辑</el-button>
          <el-button type="danger" @click="del(scope.row.id)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
// 删除请求
import { dellist } from "../../../utils/request";

import { successAlert, warningAlert } from "../../../utils/alert";

export default {
  computed: {
    ...mapGetters({
      menuList: "menu/list",
    }),
  },
  methods: {
    ...mapActions({
      responseList: "menu/responseList",
    }),
    del(id) {
      this.$confirm("你确定要删除吗？", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
      })
        .then(() => {
          dellist({ id: id }).then((res) => {

          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除",
          });
        });
    },
    // 自定义事件通知父组件menu
    edit(id) {
      this.$emit("edit", id);
    },
  },
  data() {
    return {
      value: false,
    };
  },
  mounted() {
    this.responseList();
  },
};
</script>

<style>
</style>