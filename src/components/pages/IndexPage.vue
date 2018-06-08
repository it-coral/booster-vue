<template>
    <ContentGridSimple :active="0">
        <template slot="content">
            <el-row :span="10">
                <OrderForm/>
            </el-row>
            <el-row :span="14">
                <Faq/>
            </el-row>
        </template>
    </ContentGridSimple>
</template>

<script>
import ContentGridSimple from '@/components/layouts/ContentGridSimple.vue';
import Faq from '@/components/Faq.vue';
import OrderForm from '@/components/OrderForm.vue';
import Cart from '@/components/Cart.vue';
import { Button, Row, Col } from 'element-ui';

export default {
  name: 'IndexPage',
  components: {
    'el-row': Row,
    'el-col': Col,
    Button,
    Cart,
    ContentGridSimple,
    Faq,
    OrderForm,
  },
};
</script>
