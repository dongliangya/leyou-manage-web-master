<template>
  <v-card>
      <v-flex xs12 sm10>
        <v-tree   url="/item/category/list"
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
        // treeData: treeData,
        isEdit:true
        // leafNode:[],
      }
    },
    methods: {
      handleAdd(node) {
        console.log(node)
        if (node.parentId !== 0) {
            this.$http({
              method: 'post',
              url: '/item/category',
              data: this.$qs.stringify(node)
            }).then(() => {
              this.reloadData(node.parentId);
            }).catch();
          
        }else {
          this.$message.error("刷新后重试！");
        }
      },
      handleEdit(id,name) {
        console.log(name)
        // const node={
        //   id:id,
        //   name:name
        // };
        // this.verify().then(() => {
        //   this.$http({
        //     method: 'put',
        //     url: '/item/category',
        //     data: this.$qs.stringify(node)
        //   }).then(() => {
        //     this.$message.info("修改成功！");
        //   }).catch(() => {
        //     this.$message.info("修改失败！");
        //   });
        // }).catch(() => {
        //   this.$router.push("/login");
        // });
      },
      handleDelete(id) {
        // this.verify().then(() => {
        //   this.$http.delete("/item/category/cid/" + id).then(() => {
        //     this.$message.info("删除成功！");
        //   }).catch(() => {
        //     this.$message.info("删除失败！");
        //   })
        // }).catch(() => {
        //   this.$router.push("/login");
        // });
      },
      handleClick(node) {
        //console.log(node)
      },
      reloadData(id){
        
        this.$http.get("/item/category/list?pid="+id).then().catch();
      }
    }
  };
</script>

<style scoped>

</style>
