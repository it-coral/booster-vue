<template>
    <div id="app">
        <router-view/>
    </div>
</template>

<style lang="less">
    @import 'assets/main.css';
    @import 'assets/elementui.css';
    @import 'assets/vue.css';


    .el-checkbox+.el-checkbox {
      margin-left: 0px !important;
    }

    .el-slider {
      .el-slider__runway {
        background-color: #409EFF;
        height: 8px;
      }
    }

    .el-button.el-button--primary {
      background-color: #1d1d1d !important;
      border: 3px solid #34b2f1 !important;
    }

    .text-center {
      text-align: center;
    }
</style>
