<template>
  <el-tree :data="menus" :props="defaultProps" node-key="catId" ref="menuTree" @node-click="nodeclick">
  </el-tree>
</template>

<script>
export default {
  name: "RenrenFastVueCategory",

  data() {
    return {
      menus: [],
      expandedKey: [],
      defaultProps: {
        children: "children",
        label: "name",
      },
    };
  },
  methods: {
        getMenus() {
      this.$http({
        url: this.$http.adornUrl("/product/pmscategory/list/tree"),
        method: "get",
      }).then(({ data }) => {
        console.log("成功获取到菜单数据...", data.data);
        this.menus = data.data;
      });
    },
      nodeclick(data,node,component){
    console.log("子组件category的节点被点击",data,node,component);
    // 向父组件发送事件
    this.$emit("tree-node-click",data,node,component)
  },
  },

  // 生命周期-创建完成（可以访问当前this实例）
  created() {
    this.getMenus();
  },
  // 生命周期-挂载完成（可以访问DOM元素）
  mounted() {},
  // 生命周期-创建之前
  beforeCreate() {},
  // 生命周期-挂载之前
  beforeMount() {},
  // 生命周期-更新之前
  beforeUpdate() {},
  // 生命周期-更新之后
  updated() {},
  // 生命周期-销毁之前
  beforeDestroy() {},
  // 生命周期-销毁完成
  destroyed() {},
  // 如果页面在keep-alive缓存功能， 这个函数会触发
  activated() {},
};
</script>

<style lang="scss" scoped>
</style>