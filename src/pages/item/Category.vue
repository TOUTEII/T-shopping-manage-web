<template>
  <v-card>
      <v-flex xs12 sm10>
        <v-tree url="/item/category/list"
                :isEdit="isEdit"
                @handleAdd="handleAdd"
                @handleEdit="handleEdit"
                @handleDelete="handleDelete"
                @handleClick="handleClick"
        />
      </v-flex>
  </v-card>
</template>

<script>
  import {treeData} from "../../mockDB";

  export default {
    name: "category",
    data() {
      return {
        isEdit:true,
        treeData
      }
    },
    methods: {
      handleAdd(node) {
        console.log("add .... ");
        this.$http({
          method: 'post',
          url: 'item/category/add',
          data: node
        }).then(() => {

          this.$message.success("保存成功！");
        })
          .catch(() => {
            this.$message.error("保存失败！");
          });

        console.log(node);
      },
      handleEdit(id, name) {
        console.log("edit... id: " + id + ", name: " + name)
        this.$http({
          method: 'put',
          url: 'item/category/put',
          data: {"id":id,"name":name}
        }).then(() => {

          this.$message.success("削除成功！");
        })
          .catch(() => {
            this.$message.error("保存失败！");
          });
      },
      handleDelete(id) {
        console.log("delete ... " + id)
        this.$http({
          method: 'delete',
          url: 'item/category/delete',
          data: {"id":id}
        }).then(() => {

          this.$message.success("削除成功！");
        })
          .catch(() => {
            this.$message.error("保存失败！");
          });

      },
      handleClick(node) {
        console.log(node)
      }
    }
  };
</script>

<style scoped>

</style>
