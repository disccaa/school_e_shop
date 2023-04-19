<template>
    <div class="product-card">
        <div class="product-card__img"><img :src="product.image" class="card-img-top" :alt="product.title"/></div>
        <div class="title">{{ product.title }}</div>
        <div class="price">{{ product.price }}</div>
        <div class="manipulation">
            <base-button>
                В корзину
            </base-button>
            <div class="icon">
                <base-heart/>
            </div>
        </div>
    </div>
</template>

<script>
import BaseButton from "@/components/atoms/base-button/index.vue";
import BaseHeart from "@/components/atoms/heart/index.vue";

export default {
    name: "ProductCard",
    components: {BaseHeart, BaseButton},
    props: {
        product: {
            type: Object,
            required: true
        }
    }
}
</script>

<style scoped lang="scss" src="./index.scss">

</style>