<template>
    <div>
        <div class="d-flex flex-row justify-content-between bd-highlight mb-2">
            <div class="p-3">
                <span class="my-4 items">{{ '1 items in Your Cart' }}</span>
            </div>
            <div class="p-3 price">
                <span class="my-4" id="orderGrandPriceValue">{{ 'Total: £ 0' }}</span>
            </div>
            <div class="p-3">
                <b-link class="close-icon float-right" @click="$bvModal.hide('modal-cart-items')"><i class="icon-cancel"></i></b-link>
            </div>
        </div>
        <b-form class="cart-form" id="delivery">
            <b-form-row>
                <b-col class="mt-2 mb-2 mr-5 ml-2"><b-form-input id="orderFirstName" name="first-name" placeholder="First Name *" required/></b-col>
                <b-col class="mt-2 mb-2 mr-2 ml-5"><b-form-input id="orderLastName" name="last-name" placeholder="Last Name *" required/></b-col>
            </b-form-row>

            <b-form-row>
                <b-col class="mt-2 mb-2 mr-5 ml-2"><b-form-input id="orderAddress" name="address" placeholder="Address *" required/></b-col>
                <b-col class="mt-2 mb-2 mr-2 ml-5"><b-form-input id="orderCity" name="city" placeholder="City *" required/></b-col>
            </b-form-row>

            <b-form-row>
                <b-col class="mt-2 mb-2 mr-5 ml-2"><b-form-input id="orderState" name="state" placeholder="State *" required/></b-col>
                <b-col class="mt-2 mb-2 mr-2 ml-5"><b-form-input id="orderCountry" name="country" placeholder="Country *" required/></b-col>
            </b-form-row>

            <b-form-row>
                <b-col class="mt-4 mb-2 mr-5 ml-2"><b-form-input id="orderFirstName" name="zip" placeholder="Zip Code *" required/></b-col>
                <b-col class="mt-0 mb-2 mr-2 ml-5">
                    <div class="select region-option">
                        <small>Shipping Region</small>
                        <b-form-select name="region" v-model="shippingRegion" :options="options"></b-form-select>
                    </div>
                </b-col>
            </b-form-row>

            <b-form-row>
                <b-col class="mt-2 mb-2 mr-5 ml-2">
                    <div class="select type-option">
                        <small>Shipping Type</small>
                        <b-form-select id="orderType" name="type" v-model="shippingType" :options="options"></b-form-select>
                    </div>
                </b-col>
                <b-col class="mt-2 mb-2 mr-2 ml-5"></b-col>
            </b-form-row>
            <StripeForm />
            <b-button class="m-3 mt-5 p-2 cart-buttons float-left" variant="danger" @click="changeStep">Back to Shop</b-button>
            <b-button class="m-3 mt-5 p-2 cart-buttons float-right" variant="danger" id="btnNext">Next</b-button>
        </b-form>
    </div>
</template>

<script>
import StripeForm from './StripeForm';
export default {
    name: "cartForm",
    components: {
        StripeForm
    },
    data() {
        return {
            shippingRegion: '',
            shippingType: '',
            options: [
            { value: '', text: 'Select' }
            ]
        }
    },
    methods: {
        changeStep() {
            this.$emit('nextStep', 'step1');
        }
    }
}
</script>

<style lang="scss" scoped>
    .items{
        color: #2E2E2E;
        font-size: 24px;
        font-weight: 700;
    }
    .price{
        font-size: 18px;
        color: #6c6c6c;
        font-weight: 700;
    }
    .close-icon{
        font-size: 25px;
        color: red;
    }
    .cart-form{
        padding: 3%;
        box-shadow: 0 4px 6px -1px rgba(0,0,0,.1), 0 2px 4px -1px rgba(0,0,0,.06);
        input{
            padding: 25px 10px;
            box-shadow: none;
            &:focus{
                border: 2px solid rgb(245, 68, 68);
            }
        }
    }
    .select{
        small{
            position: relative;
            bottom: -13px;
        }
        select{
            border: none;
            border-bottom: 2px solid #555;
            &:focus{
                box-shadow: none;
                border-bottom: 2px solid red;
                background: rgb(221, 221, 221);
            }
        }
    }
    .cart-buttons{
        border-radius: 20px;
        font-weight: 700;
        width: 150px;
    }
    .payment-btn{
        width: 300px;
        height: 40px;
        position: relative;
        top: -40px;
        border-radius: 0;
        &:focus{
            box-shadow: none;
        }
    }
</style>