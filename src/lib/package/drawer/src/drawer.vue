<template>
  <div>
    <transition :name="placement === 'left'?'x-drawer-slide-left':'x-drawer-slide'">
      <div
        class="x-drawer"
        v-show="value"
        :class="[placement === 'left'?'x-drawer-left':'']"
        :style="{width:width || (width + 'px')}"
      >
        <div class="x-drawer-header">
          <span>{{title}}</span>
          <i class="x-iconclose" v-if="closeable" @click="close"></i>
        </div>
        <div class="x-drawer-body">
          <slot></slot>
        </div>
      </div>
    </transition>

    <transition>
      <div class="x-mask" v-show="value" @click="close"></div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "XDrawer",
  data() {
    return {};
  },
  props: {
    title: {
      type: String,
      default: ""
    },
    value: Boolean,
    placement: {
      type: String,
      default: "right"
    },
    closeable: Boolean,
    width: {
      type: String,
      default: ""
    }
  },

  methods: {
    close() {
      this.$emit("input", false);
      this.$emit("close")
    }
  },
  watch: {
    value(newVal) {
      if (newVal) {
         let top = document.scrollingElement.scrollTop
         document.onscroll = function(){
            document.scrollingElement.scrollTop = top
         }
          return;
      }
      document.onscroll = null
    }
  }
};
</script>

<style scoped>
</style>