<template>
  <div class="menu">
    <MenuItem
      v-for="(item, index) in menuTree"
      :key="index"
      :data="item.children"
      :depth="0"
      :icon="item.icon"
      :label="item.label"
    />
  </div>
</template>

<script>
import MenuItem from "@/components/MenuItem.vue";

export default {
  name: "RecursiveMenu",
  components: { MenuItem },
  data: () => ({
    menuTree: [
      {
        label: "Home",
        icon: "home",
        children: [
          {
            label: "level 1.1",
            children: [
              {
                label: "level 1.1.2",
              },
            ],
          },
          {
            label: "level 1.2",
          },
        ],
      },
      {
        label: "Dashboard",
        icon: "dashboard",
        children: [
          {
            label: "level 1",
            children: [
              {
                label: "level 1.1",
                children: [
                  {
                    label: "level 1.1.1",
                  },
                ],
              },
              {
                label: "level 1.2",
                children: [
                  {
                    label: "level 1.2.1",
                  },
                ],
              },
            ],
          },
        ],
      },
      {
        label: "Settings",
        icon: "settings",
      },
    ],
  }),
};
</script>

<style lang="scss" scoped>
.menu {
  position: fixed;
  height: 100vh;
  width: 240px;
  left: 0;
  top: 0;
  border-right: 1px solid #eceecc;
  transition: all 0.3 ease;
  overflow: auto;
}
</style>
