<template> 
  <a-layout :class="prefixCls">
    <a-layout-header v-show="false" class="header" >
    </a-layout-header>
    <a-layout-content > 
     <landing></landing>
    </a-layout-content>
    <a-layout-footer v-show="false" class="footer" >
    </a-layout-footer> 
  </a-layout> 
</template>
<script lang="ts" setup>
  import { computed } from 'vue';
  import { AppLogo } from '/@/components/Application';
  import { AppLocalePicker, AppDarkModeToggle } from '/@/components/Application';
  import { SettingOutlined, EditOutlined, DeleteOutlined, PlayCircleOutlined,EllipsisOutlined } from '@ant-design/icons-vue';
  
  import { useGlobSetting } from '/@/hooks/setting';
  import { useI18n } from '/@/hooks/web/useI18n';
  import { useDesign } from '/@/hooks/web/useDesign';
  import { useLocaleStore } from '/@/store/modules/locale';
  import { useLoginState, LoginStateEnum } from '../env/useLogin';
  import   landing   from './landing/index.vue';
  defineProps({
    sessionTimeout: {
      type: Boolean,
    },
  });

  const globSetting = useGlobSetting();
  const { prefixCls } = useDesign('website');
  const { t } = useI18n();
  const localeStore = useLocaleStore();
  const showLocale = localeStore.getShowPicker;
  const title = computed(() => globSetting?.title ?? '');
  const { handleBackLogin } = useLoginState();
  //handleBackLogin(); 
</script>
<style lang="less">
  @prefix-cls: ~'@{namespace}-website';
  @website-prefix-cls: ~'@{namespace}-app-logo';
  @countdown-prefix-cls: ~'@{namespace}-countdown-input';
  @dark-bg: #293146;
  @light-bg: #fff;
  html[data-theme='dark'] {
    .@{prefix-cls} {
      background-color: @dark-bg;


      &::before {
       // background-image: url(/@/assets/svg/login-bg-dark.svg);
      }

      .ant-input,
      .ant-input-password {
        background-color: #232a3b;
      }

      .ant-btn:not(.ant-btn-link):not(.ant-btn-primary) {
        border: 1px solid #4a5569;
      }

      &-form {
        background: transparent !important;
      }

      .app-iconify {
        color: #fff;
      }
    }

    input.fix-auto-fill,
    .fix-auto-fill input {
      -webkit-text-fill-color: #c9d1d9 !important;
      box-shadow: inherit !important;
    }
  }

  .header {
        background: transparent !important;
  }
  .@{prefix-cls} {
    min-height: 100%;
    overflow: hidden;
    background-color: @light-bg;
    @media (max-width: @screen-xl) {
      background-color: #293146;

      .@{prefix-cls}-header {
        background-color: @light-bg;
      }
    }
 

    &::before {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      margin-left: -48%;
   //    background-image: url(/@/assets/svg/login-bg.svg);
      background-position: 100%;
      background-repeat: no-repeat;
      background-size: auto 100%;
      content: '';
      @media (max-width: @screen-xl) {
        display: none;
      }
    }

    .@{website-prefix-cls} {
      position: absolute;
      top: 12px;
      height: 30px;

      &__title {
        font-size: 16px;
        color: #fff;
      }

      img {
        width: 32px;
      }
    }

 

    
  }
</style>
