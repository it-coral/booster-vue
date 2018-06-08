<template>
    <div>
        <header>
            <div class="menu">
                <span class="menu-item" v-for="item in menus" :key="item.value">
                    <a v-bind:href="item.link" :class="item.value != 'LOGIN' ? 'menu-link' : 'menu-link login-menu-link'">{{item.value}}</a>
                </span>
            </div>
            <div class="menu">
                <img class="header-logo" v-bind:src="logoPath" />
            </div>
        </header>
        <main>
            <div id="steps-bar">
                <div class="steps-bar-title">
                  <span>{{steps[active].name}}</span>
                </div>
                <Steps :active="active" finish-status="success">
                    <Step />
                    <Step />
                    <Step />
                    <Step />
                    <Step />
                </Steps>
            </div>
            <div id="content-grid-simple">
                <!-- <LoginBar /> -->
                <slot name="content"/>
                <div id="buttons-bar">
                    <slot name="buttons"/>
                </div>
            </div>
        </main>
    </div>
</template>

<script>
import { Button, ButtonGroup, Steps, Step } from 'element-ui';
import LoginBar from '@/components/LoginBar.vue';
import logoImage from '@/assets/logo.png';

export default {
  name: 'ContentGrid',
  props: {
    active: 0,
  },
  data: () => ({
    steps: [
      { name: 'Select your package' },
      { name: 'Checkout' },
      { name: 'Confirm order' },
      { name: 'Payment' },
      { name: 'Finish' }],
  }),
  components: {
    Button, ButtonGroup, LoginBar, Steps, Step,
  },
  data() {
    return {
      menus: [
        {
          link: '/about',
          value: 'ABOUT',
        },
        {
          link: '/contact',
          value: 'CONTACT',
        },
        {
          link: '/faq',
          value: 'FAQ',
        },
        {
          link: '/login',
          value: 'LOGIN',
        },
      ],
      logoPath: logoImage,
    };
  },
};
</script>
<<<<<<< HEAD
<style lang="less">
.steps-bar-title {
  font-size: 20px;
  font-weight: 600;
  text-transform: uppercase;

  display: flex;
  justify-content: center;
  align-items: center;

  margin: 50px 0;
}

@main-blue: #409EFF;
@main-blue-dark: #409EFF;
.el-step {
  .el-step__head {
    .el-step__line {
      height: 4px;
      top: 20px;
      .el-step__line-inner {
        color: #0a0a0a;
      }
    }
    .el-step__icon {
      border-radius: 1px;
      width: 45px;
      height: 45px;

      background: #1b1b1b;
      border: 2px solid @main-blue;
    }
    .el-step__icon-inner {
      font-size: 30px;
      font-weight: 800;
      color: #f9f9f9;
    }

    &.is-wait {
      opacity: 0.3;
      .el-step__icon {
        background: #c6c6c6;
        border: 2px solid @main-blue;
      }
      .el-step__icon-inner {
        color: #d7d7d7;
      }
    }
  }
}
=======

<style lang="less">
    .menu {
        text-align: center;
        margin: 3em 0;
    }

    .menu-item {
        margin: 0 2em;
    }

    .menu-link {
        color: white;
        text-decoration: none;
    }

    .login-menu-link {
        background: #00b4ff;
        padding: .5em;
    }

    .header-logo {
        width: 350px;
        margin-top: 2em;
    }
>>>>>>> c16877d507775e0d5f228239e9968ed77eb35d97
</style>
