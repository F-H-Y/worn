<!--
 * @Description: 设置页面
 * @Author: ZY
 * @Date: 2020-12-17 16:05:05
 * @LastEditors: ZY
 * @LastEditTime: 2021-01-27 13:48:18
-->
<template>
  <div class="drawer-container">
    <div class="word">
      <div class="word_left">
        <!-- <img src="" alt=""> -->
      </div>
      <div class="word_right">
        <div class="right_top">
          <div class="right_title">
            温馨提示
          </div>
          <div class="right_guan">
            ×
          </div>
        </div>
        <div class="right_bottom">
          一年一度的消夏晚会即将开启，大家不要错过噢...
        </div>
      </div>
    </div>

    <div class="news-bottom">
        <div class="news-bottom-one">
          <!-- 点击事件 @click="onClickMenu(item)" -->
          <div v-for="(item,index) in lists" :key="index" >
            <i class="iconfont" :class="item.icon"></i>
            <text>{{item.title}}</text>
          </div>
        </div>
      </div>
  </div>
</template>

<script lang="ts">
import { useStore } from '@/store'
import { SettingsActionTypes } from '@/store/modules/settings/action-types'
import { defineComponent, reactive, toRefs, watch } from 'vue'
// import ThemePicker from '@/components/theme-picker/Index.vue'
import { useI18n } from 'vue-i18n'

export default defineComponent({
  components: {
    // ThemePicker
  },
  setup() {
    const lists = [
      { type: '规章制度', icon: 'el-icon-tickets' },
      { type: '个人资料', icon: 'el-icon-document-remove' },
      { type: '集团文件', icon: 'el-icon-document-copy' },
      { type: '流程汇总', icon: 'el-icon-help' },
      { type: '活动', icon: 'el-icon-coordinate' },
      { type: '消息', icon: 'el-icon-chat-line-square' },
      { type: '任务', icon: 'el-icon-document-checked' }
    ]
    const store = useStore()
    const { t } = useI18n()
    const state = reactive({
      fixedHeader: store.state.settings.fixedHeader,
      showTagsView: store.state.settings.showTagsView,
      showSidebarLogo: store.state.settings.showSidebarLogo,
      sidebarTextTheme: store.state.settings.sidebarTextTheme,
      themeChange: (value: string) => {
        store.dispatch(SettingsActionTypes.ACTION_CHANGE_SETTING, { key: 'theme', value })
      }
    })

    watch(() => state.fixedHeader, (value) => {
      store.dispatch(SettingsActionTypes.ACTION_CHANGE_SETTING, { key: 'fixedHeader', value })
    })

    watch(() => state.showTagsView, (value) => {
      store.dispatch(SettingsActionTypes.ACTION_CHANGE_SETTING, { key: 'showTagsView', value })
    })

    watch(() => state.showSidebarLogo, (value) => {
      console.log(value)

      store.dispatch(SettingsActionTypes.ACTION_CHANGE_SETTING, { key: 'showSidebarLogo', value })
    })

    watch(() => state.sidebarTextTheme, (value) => {
      store.dispatch(SettingsActionTypes.ACTION_CHANGE_SETTING, { key: 'sidebarTextTheme', value })
    })

    return {
      t,
      ...toRefs(state),
      lists
    }
  }
})
</script>

<style lang="scss" scoped>
.drawer-container {
  padding: 35px;
  font-size: 14px;
  line-height: 1.5;
  word-wrap: break-word;
  padding-top:40px;

  .drawer-title {
    margin-bottom: 12px;
    color: rgba(0, 0, 0, .85);
    font-size: 14px;
    line-height: 22px;
  }

  .drawer-item {
    color: rgba(0, 0, 0, .65);
    font-size: 14px;
    padding: 12px 0;
  }

  .drawer-switch {
    float: right
  }

  .word{
    display: flex;
    justify-content: space-between;
    background:rgb(24, 144, 255);
    border-radius:5px;
    color:#fff;
    padding:10px;
    .word_left{
      width:44px;
      height:44px;
    }
    .word_right{
      .right_top{
        display: flex;
        justify-content: space-between;
        font-size:20px;
        padding-top:5px;
        .right_guan{
          font-size:30px;
          padding-top:0;
          line-height: 0.6;
        }
      }
      .right_bottom{
        font-size:16px;
        padding-bottom:5px;
      }
    }

  }

  .news-bottom {
    position: absolute;
    bottom: 0;
    width: 390px;
    height: 126px;
    .new-bottom-one{
      display: flex;
      flex-wrap:wrap;
      justify-content: center;
      div{
        width: 86px;
        height: 58px;
        background-color: #616161;
        margin: 2px 2px;
        display: flex;
        flex-direction: column;
        color: #fff;
        padding: 6px;
        font-size: 14px;
        text-align:center;
      }
    }
  }
}

</style>
