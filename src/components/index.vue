<template>
  <div class="whole">
    <!-- top -->
    <div class="top"></div>
    <!-- left -->
    <div class="left">
      <ul class="nav">
        <li v-for="(item,index) in nav" :key="item.title">
          <div class="flex flex_j_b flex_a_c" :class="{bg_color:item.open,font_fff:item.open}" nth="1" @click="changeTab(1,index)">
            {{item.title}}
            <i v-if="item.list && !item.open" class="el-icon-arrow-down"></i>
            <i v-if="item.list && item.open" class="el-icon-arrow-up"></i>
          </div>
          <ul class="nav" v-if="item.list && item.open">
            <li v-for="(itm,idx) in item.list" :key="itm.title">
              <div class="flex flex_j_b flex_a_c" nth="2" @click="changeTab(2,index,idx)">
                {{itm.title}}
                <i v-if="itm.list && !itm.open" class="el-icon-arrow-down"></i>
                <i v-if="itm.list && itm.open" class="el-icon-arrow-up"></i>
              </div>
              <ul class="nav" v-if="itm.list && itm.open">
                <li v-for="(its,ix) in itm.list" :key="its.title">
                  <div
                    class="flex flex_j_b flex_a_c"
                    nth="2"
                    @click="changeTab(3,index,idx,ix)"
                  >{{its.title}}</div>
                </li>
              </ul>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: "hello",
  data() {
    return {
      nav: [
        {
          title: "主菜单",
          open: false
        },
        {
          title: "组织架构",
          open: false,
          list: [
            {
              title: "部门管理",
              open: false,
              list: [
                {
                  title: "部门列表",
                  open: false
                },
                {
                  title: "添加部门",
                  open: false
                }
              ]
            },
            {
              title: "职位管理",
              open: false
            },
            {
              title: "员工管理",
              open: false
            }
          ]
        }
      ]
    };
  },
  methods: {
    changeTab(e, ...index) {
      var th = this;
      console.log(index);
      if (e == 1) {
        //第一层，展开或关闭第二层
        th.nav[index[0]].open = !th.nav[index].open;
      } else if (e == 2) {
        th.nav[index[0]].list[index[1]].open = !th.nav[index[0]].list[index[1]]
          .open;
      }
    }
  }
};
</script>
<style scoped>
@import url("../assets/css/index.css");
</style>