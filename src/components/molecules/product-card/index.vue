<template>
    <div class="product-card">
        <div class="product-card__view">
          <div class="product-card__view__img">
            <img :src="product.image" style="width: 200px" :alt="product.title"/>
          </div>
          <button class="product-card__view__btn">Быстрый просмотр</button>
        </div>

        <div class="product-card__info">
          <h2 class="product-card__info__title">{{ product.title }}</h2>
          <div class="scroll">
            <div class="product-card__info__desc">{{product.description}}</div>
          </div>

        </div>
        <div class="product-card__purchase">
          <div class="product-card__purchase__price">
            <div class="purchase__price__sale">
              <span class="sale-price">{{currencyValidation(product.price)}}</span>
              <span class="sale-sum">Скидка {{currencyValidation(saleSum)}}</span>
            </div>
            <div class="purchase__price__real">{{currencyValidation(salePrice)}}</div>

          </div>
          <div class="manipulation">
            <base-button variant="white">Добавить в корзину</base-button>
            <base-button variant="black">Узнать больше</base-button>
          </div>
        </div>


    </div>
</template>

<script>
import BaseButton from "@/components/atoms/base-button/index.vue";
import BaseHeart from "@/components/atoms/heart/index.vue";
import {currencyValidation} from "@/helpers/numberFormater";
import {computed} from "vue";
export default {
    name: "ProductCard",
    components: {BaseHeart, BaseButton},
    props: {
        product: {
            type: Object,
            required: true
        }

    },
    setup(props){
      const saleSum = computed(()=> {
         return props.product.price*0.1;
      })
      const salePrice = computed(()=>{
        return props.product.price*0.9;
      })

      return {currencyValidation, salePrice, saleSum}

    }


}
</script>

<style scoped lang="scss" src="./index.scss">

</style>