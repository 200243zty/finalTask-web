<template>
  <div class="sidebar">
    <el-menu
      class="sidebar-el-menu"
      :default-active="OnRoutes"
      :collapse="collapse"
      background-color="#334256"
      text-color="#fff"
      active-text-color="#20a0ff"
      router
    >
      <template v-for="item in items">
        <template>
          <el-menu-item :index="item.index" :key="item.index">
            <i :class="item.icon"></i>
            {{ item.title }}
          </el-menu-item>
        </template>
      </template>
    </el-menu>
  </div>
</template>

<script>
import bus from "../assets/js/bus";
export default {
  name: "TheAside",
  data() {
    return {
      collapse: false, // 折叠属性
      items: [
        {
          icon: "el-icon-setting",
          index: "Info",
          title: "系统",
        },
        {
          icon: "el-icon-user",
          index: "Consumer",
          title: "用户",
        },
        {
          icon: "el-icon-s-custom",
          index: "Singer",
          title: "歌手",
        },
        {
          icon: "el-icon-s-management",
          index: "SongList",
          title: "歌单",
        }
      ],
    };
  },
  computed: {
    OnRoutes() {
      return this.$route.path.replace("/", "");
    },
  },
  created() {
    bus.$on("collapse", (msg) => {
      this.collapse = msg;
    });
  },
};
</script>

<style scoped>
.sidebar {
  display: block;
  position: absolute;
  left: 0;
  top: 70px;
  bottom: 0;
  background-color: #334256;
  overflow-y: scroll;
}
.sidebar::-webkit-scrollbar {
  width: 0;
}
.sidebar-el-menu:not(.el-menu--collapse) {
  width: 150px;
}
.sidebar > ul {
  height: 100%;
}
</style>
