<template>
    <div id="order-form">
        <el-row :gutter="30">
            <el-col :span="12">
                <fieldset id="mode-field" class="seclection-group">
                    <legend>Competitive Mode</legend>

                    <RadioGroup v-model="mode">
                        <Radio :label="'solo'">Solo</Radio>
                        <Radio :label="'duo'">Duo</Radio>
                        <Radio :label="'squad'">Squad</Radio>
                    </RadioGroup>

                    <!-- <div class="form-radio">
                        <label for="mode-solo">
                            <input type="radio" @change="updateTotal" v-model="mode" value="solo" id="mode-solo" checked>
                            <label for="mode-solo" class="custom-checkbox"></label>Solo
                        </label>
                    </div>

                    <div class="form-radio">
                        <label for="mode-duo">
                            <input type="radio" @change="updateTotal" v-model="mode" value="duo" id="mode-duo">
                            <label for="mode-duo" class="custom-checkbox"></label>Duo
                        </label>
                    </div>

                    <div class="form-radio">
                        <label for="mode-squad">
                            <input type="radio" @change="updateTotal" v-model="mode" value="squad" id="mode-squad">
                            <label for="mode-squad" class="custom-checkbox"></label>Squad
                        </label>
                    </div> -->
                </fieldset>
            </el-col>

            <el-col :span="12">
                <fieldset id="platform-field" class="seclection-group">
                    <legend>Platform</legend>

                    <RadioGroup v-model="platform">
                        <Radio :label="'pc'">PC</Radio>
                        <Radio :label="'ps4'">PS4</Radio>
                        <Radio :label="'xbox'">Xbox</Radio>
                    </RadioGroup>

                    <!-- <div class="form-radio">
                        <label for="platform-pc">
                            <input type="radio" @change="updateTotal" v-model="platform" value="pc" id="platform-pc" checked>
                            <label for="platform-pc" class="custom-checkbox"></label>PC
                        </label>
                    </div>

                    <div class="form-radio">
                        <label for="platform-ps4">
                            <input type="radio" @change="updateTotal" v-model="platform" value="ps4" id="platform-ps4">
                            <label for="platform-ps4" class="custom-checkbox"></label>PS4
                        </label>
                    </div>

                    <div class="form-radio">
                        <label for="platform-xbox">
                            <input type="radio" @change="updateTotal" v-model="platform" value="xbox" id="platform-xbox">
                            <label for="platform-xbox" class="custom-checkbox"></label>Xbox
                        </label>
                    </div> -->
                </fieldset>
            </el-col>
        </el-row>


        <el-row :gutter="30">
            <el-col :span="12">
                <fieldset id="quantity-field" class="seclection-group">
                    <legend>Wins</legend>
                    <el-slider @change="updateTotal" :min="1" v-model="quantity"/>
                    <div id="quantity-value">{{ quantity }} wins</div>
                </fieldset>
            </el-col>
            <el-col :span="12">
                <fieldset id="specials-field" class="seclection-group">
                    <legend>Specials</legend>

                    <Checkbox v-model="end9">End game with 9 or more kills</Checkbox>
                    <Checkbox v-model="stream">Stream my boost</Checkbox>
                    <Checkbox v-model="oldbooster">I want my old booster</Checkbox>
                    <Checkbox v-model="playwithbooster">I want to play with booster</Checkbox>

                    <!--
                    <label for="specials-end9">
                        <input type="checkbox" @change="updateTotal" v-model="end9" id="specials-end9">
                        <label for="specials-end9" class="custom-checkbox"></label>End game with 9 or more kills
                    </label>

                    <label for="specials-stream">
                        <input type="checkbox" @change="updateTotal" v-model="stream" id="specials-stream">
                        <label for="specials-stream" class="custom-checkbox"></label>Stream my boost
                    </label>

                    <label for="specials-oldbooster">
                        <input type="checkbox" @change="updateTotal" v-model="oldbooster" id="specials-oldbooster">
                        <label for="specials-oldbooster" class="custom-checkbox"></label>I want my old booster
                    </label> -->
                </fieldset>
            </el-col>
        </el-row>

        <el-row justify="center" type="flex">
            <div id="checkout">
                <div id="total-amount" class="text-bottom-border">TOTAL:</div>
                <div id="total-amount" class="text-bottom-border">{{ currentTotal }}</div>
            </div>
        </el-row>

        <el-row>
            <div id="buttons-bar">
                <Button @click="addToCart" type="primary">Add to Cart</Button>
                <Button @click="checkout" :disabled="checkoutDisabled" type="primary">
                    <i class="el-icon-goods"></i>
                    Checkout
                </Button>
            </div>
        </el-row>

        <!-- <p id="get-started">
            Contact us on Skype using the button below.
        </p> -->

        <!-- <div id="skype-bar">
            <a id="skype-button" href="skype:elojobbing?chat">
                <img src="@/assets/chatbutton_32px.png">
            </a>
        </div> -->
    </div>
</template>

<script>
import { Button, Notification, Row, Col, Radio, RadioGroup, Checkbox } from 'element-ui';
import { getPrice } from '@/store/cart';

export default {
  name: 'OrderForm',
  components: {
    Button,
    RadioGroup,
    Radio,
    Checkbox,
    'el-row': Row,
    'el-col': Col,
  },
  data: () => ({
    mode: 'solo',
    platform: 'pc',
    quantity: 10,
    end9: false,
    stream: false,
    oldbooster: false,
    playwithbooster: false,
    specials: [],
    discount: 0,
    total: 0,
  }),
  watch: {
    mode: () => { this.updateTotal(); },
    platform: () => { this.updateTotal(); },
    quantity: () => { this.updateTotal(); },
    end9: () => { this.updateTotal(); },
    stream: () => { this.updateTotal(); },
    oldbooster: () => { this.updateTotal(); },
    playwithbooster: () => { this.updateTotal(); },
  },
  props: {},
  methods: {
    getItem() {
      const specials = ['end9', 'stream', 'oldbooster', 'playwithbooster'].map(s => (this[s] ? s : null)).filter(n => n);

      return {
        game: 'fortnite',
        product_id: 1,
        mode: this.mode,
        platform: this.platform,
        quantity: this.quantity,
        specials,
      };
    },

    updateTotal() {
      this.total = getPrice(this.getItem(), this.discount);
    },

    addToCart() {
      this.$store.dispatch('cart/add', this.getItem());

      Notification.success({
        title: 'Add to Cart',
        message: 'You have added an item to the cart',
      });
    },

    checkout() {
      this.$router.push('checkout');
    },
  },
  computed: {
    currentTotal() {
      return `$${this.total.toFixed(2)}`;
    },
    checkoutDisabled() {
      return this.$store.getters['cart/items'].length === 0;
    },
  },
  mounted() {
    this.updateTotal();
  },


};
</script>

<style scoped lang="less">
    #get-started {
        font-size: 1em;
        font-weight: 500;
        margin-top: 2em;
    }

    #buttons-bar, #skype-bar {
        text-align: center;
    }

    .text-bottom-border {
        border-bottom: 1px solid #d8dbe2;
        padding: 0px 40px;
    }

    .seclection-group {
        legend {
            margin: 20px 0px;
        }
        margin: 0px 0px 40px 0px;
    }
</style>
