<!--
 * @Description:
 * @Author: ZY
 * @Date: 2020-12-24 10:44:01
 * @LastEditors: ZY
 * @LastEditTime: 2021-03-25 08:27:00
-->

<template>
  <div
    class="handle-button"
    :style="{'top': buttonTop+'px','backgroundColor': theme}"
    @click="show= true"
  >
    <i class="el-icon-chat-dot-round" />
    <!-- <text>消息提示</text> -->
  </div>
  <el-drawer
    title="消息提示"
    v-model="show"
    size="400px"
    :direction="direction"
    destroy-on-close
  >
    <slot />
  </el-drawer>
</template>

<script lang="ts">
import { useStore } from '@/store'
import { computed, defineComponent, ref } from 'vue'
export default defineComponent({
  props: {
    buttonTop: {
      type: Number,
      default: 250
    }
  },
  setup() {
    const show = ref(false)
    const store = useStore()
    const theme = computed(() => {
      return store.state.settings.theme
    })
    return {
      show,
      theme
    }
  }
})
</script>

<style lang="scss" >

.handle-button {
  width:60px;
  height: 60px;
  position: fixed;
  top:0;
  right: 0px;
  text-align: center;
  font-size: 24px;
  border-radius: 6px 0 0 6px !important;
  z-index: 99;
  cursor: pointer;
  pointer-events: auto;
  color: #fff;
  line-height: 30px;
  display:flex;
  flex-flow: column;
  text-align:center;
  i {
    font-size: 36px;
    line-height: 60px;
  }
  // text{
  //   display: block;
  // }
}
.el-drawer__header {
  margin:15px;
  margin-bottom: 0px !important;
  font-size:25px;

}

</style>
