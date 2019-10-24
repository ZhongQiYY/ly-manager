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
  export default {
    name: "category",
    data() {
      return {
        isEdit:true
      }
    },
    methods: {
      handleAdd(node) {
        console.log("add............");
        console.log(node);
        this.$http({
          method: 'post',
          url:'/item/category/save',
          data:this.$qs.stringify(node)
        }).then().catch();
      },
      handleEdit(id, name) {
        console.log("edit... id: " + id + ", name: " + name);
        const node = {
          id : id,
          name : name
        };
        this.$http({
          method: 'put',
          url: '/item/category/edit',
          data:this.$qs.stringify(node)
        }).then(() => {
          this.$message.info("修改成功");
        }).catch(() => {
          this.$message.info("修改失败");
        })
      },
      handleDelete(id) {
        console.log("delete ... " + id);
        this.$http({
          method: 'delete',
          url:'/item/category/delete/'+id
        }).then(() => {
          this.$message.info("删除成功");
        }).catch(() => {
          this.$message.info("删除失败");
        })
      },
      handleClick(node) {
        console.log(node)
      }
    }
  };
</script>

<style scoped>

</style>
