<template>
  <div class="sidebar">
    <el-menu
        class="sidebar-el-menu"
        :default-active="onRoutes"
        background-color="#324157"
        text-color="#bfcbd9"
        active-text-color="#20a0ff"
        unique-opened
        router
    >
      <template v-for="item in items">
        <template v-if="item.subs">
          <el-submenu :index="item.index" :key="item.index">
            <template #title>
              <i :class="item.icon"></i>
              <span>{{ item.title }}</span>
            </template>
            <template v-for="subItem in item.subs">
              <el-submenu
                  v-if="subItem.subs"
                  :index="subItem.index"
                  :key="subItem.index"
              >
                <template #title>{{ subItem.title }}</template>
                <el-menu-item
                    v-for="(threeItem, i) in subItem.subs"
                    :key="i"
                    :index="threeItem.index"
                >{{ threeItem.title }}
                </el-menu-item>
              </el-submenu>
              <el-menu-item
                  v-else
                  :index="subItem.index"
                  :key="subItem.index"
              >{{ subItem.title }}
              </el-menu-item>
            </template>
          </el-submenu>
        </template>
        <template v-else>
          <el-menu-item :index="item.index" :key="item.index">
            <i :class="item.icon"></i>
            <template #title>{{ item.title }}</template>
          </el-menu-item>
        </template>
      </template>
    </el-menu>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          icon: "el-icon-s-home",
          index: "home",
          title: "首页"
        },
        {
          icon: "el-icon-date",
          index: "2",
          title: "图书管理",
          subs: [
            {
              index: "bookList",
              title: "图书列表"
            },
            {
              index: "addBook",
              title: "添加图书"
            }
          ]
        },
        {
          icon: "el-icon-pie-chart",
          index: "3",
          title: "借阅统计",
          subs: [
            {
              index: "userReadList",
              title: "个人借阅排行"
            },
            {
              index: "readList",
              title: "书籍借阅排行"
            }
          ]
        },
        {
          icon: "el-icon-time",
          index: "log",
          title: "借还日志"
        },
        {
          icon: "el-icon-s-custom",
          index: "about",
          title: "个人中心"
        },
      ]
    };
  },
  computed: {
    onRoutes() {
      return this.$route.path.replace('/admin/','');
    }
  }
};
</script>

<style scoped>

</style>
