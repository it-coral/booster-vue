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
                <Steps :active="active" finish-status="success">
                    <Step title="Choose your package"/>
                    <Step title="Checkout"/>
                    <Step title="Confirm order"/>
                    <Step title="Payment"/>
                    <Step title="Finish"/>
                </Steps>
            </div>
            <div id="content-grid-simple">
                <LoginBar />
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
</style>
