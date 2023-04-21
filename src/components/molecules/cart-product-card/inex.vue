<template>
    <div class="product-card-cart">
        <div class="cart-left">
            <div class="cart-left__image">
                <img :src="product.image"
                     :alt="product.title">
            </div>
            <div class="cart-left__info info">
                <div class="info__title"> {{ product.title }}</div>
                <div class="info__count">
                    <cart-count v-model="count"/>
                </div>
            </div>
        </div>
        <div class="cart-right">
            <div class="sum">
                <div class="total-sum">
                    {{ currencyValidation(Math.floor(product.price * count * 0.9)) }}
                </div>
                <div class="discount">
                    <span>{{ currencyValidation(Math.floor(product.price * count)) }}</span>
                    <span>Выгода({{ currencyValidation(Math.floor(product.price * count * 0.1)) }})</span>
                </div>
                <div class="initial-price">{{ product.price }}</div>
            </div>
            <div class="delete">
                <icon-bin/>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "CartProductCard"
}
</script>
<script setup>
import IconBin from '@/assets/icons/bin.svg?component'
import CartCount from "@/components/atoms/cart-count/index.vue";
import {ref} from "vue";
import {currencyValidation} from "../../../helpers/numberFormater";

const props = defineProps({
    product: {
        type: Object,
        default: () => {
            return {
                id: 3,
                title: "Смартфон Apple iPhone 13 4/128GB Pink",
                price: 482016,
                category: 2,
                image: "http://localhost:8000/media/images/products/6af20553-8e9d-4654-9b04-242eee81f99b.webp",
                count: 1
            }
        }
    }
})
const test = {
    id: 3,
    title: "Смартфон Apple iPhone 13 4/128GB Pink",
    price: 482016,
    category: 2,
    image: "http://localhost:8000/media/images/products/6af20553-8e9d-4654-9b04-242eee81f99b.webp",
    count: 1
}
const count = ref(props.product.count)
</script>

<style scoped lang="scss" src="./index.scss"/>

