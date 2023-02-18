<template>
  <div :class="{ expanded }" class="menu-item">
    <div
      :style="{
        paddingLeft: depth * 20 + 20 + 'px',
      }"
      class="label"
      @click="toggleMenu()"
    >
      <div class="left">
        <i v-if="icon" class="material-symbols-outlined">{{ icon }}</i>
        <span>{{ label }}</span>
      </div>
      <div v-show="data" class="right">
        <i :class="{ expanded }" class="material-symbols-outlined expand"
          >expand_more</i
        >
      </div>
    </div>
    <div
      v-if="showChildren"
      ref="container"
      :style="{ height: containerHeight }"
      class="items-container"
    >
      <MenuItem
        v-for="(item, index) in data"
        :key="index"
        :data="item.children"
        :depth="depth + 1"
        :icon="item.icon"
        :label="item.label"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "MenuItem",
  data: () => ({
    showChildren: false,
    expanded: false,
    containerHeight: 0,
  }),
  props: {
    label: {
      type: String,
      required: true,
    },
    icon: {
      type: String,
    },
    depth: {
      type: Number,
      required: true,
    },
    data: {
      type: Array,
    },
  },
  methods: {
    toggleMenu() {
      this.expanded = !this.expanded;
      if (!this.showChildren) {
        this.showChildren = true;
        this.$nextTick(() => {
          this.containerHeight = this.$refs["container"].scrollHeight + "px";
          setTimeout(() => {
            this.containerHeight = "fit-content";
            this.$refs["container"].style.overflow = "visible";
          }, 300);
        });
      } else {
        this.containerHeight = this.$refs["container"].scrollHeight + "px";
        this.$refs["container"].style.overflow = "hidden";
        setTimeout(() => {
          this.containerHeight = 0 + "px";
        }, 10);
        setTimeout(() => {
          this.showChildren = false;
        }, 300);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.menu-item {
  position: relative;
  width: 100%;

  .label {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    white-space: nowrap;
    user-select: none;
    height: 50px;
    padding: 0 20px;
    box-sizing: border-box;
    color: #6a6a6a;
    transition: all 0.3s ease;

    > div {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    i {
      font-size: 20px;
      color: #6e6e6e;
      transition: all 0.3s ease;

      &.expand {
        font-size: 16px;
        color: #cacaca;

        &.expanded {
          transform: rotate(180deg);
        }
      }
    }

    &:hover {
      background-color: #deedff;
      cursor: pointer;
    }
  }

  .items-container {
    width: 100%;
    overflow: hidden;
    transition: height 0.3s ease;
  }
}
</style>
