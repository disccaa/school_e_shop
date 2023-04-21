<script setup>
import { ref, watch} from 'vue'
import {useRoute} from 'vue-router'
import cartMethods from '../utils/cart'
import ProductCard from "@/components/molecules/product-card/index.vue";
import ADialog from "@/components/atoms/dialog/index.vue";
import PaginationButton from "@/components/atoms/pagination/index.vue";
import {UseFetchProducts} from "@/composebles/fetch";
import CartProductCard from "@/components/molecules/cart-product-card/inex.vue";

const route = useRoute()
const {data, totalPages, params, page} = UseFetchProducts()


watch(route,   async () => {
    params.value = {...route.query}

}, {immediate:true})


const isOpen = ref(true)
</script>
<template>

    <a-dialog v-model="isOpen">
    </a-dialog>
    <h1>Products</h1>˜
    <div class="container">
        <cart-product-card/>
        <pagination-button :total-page="totalPages" v-model="page"/>
        {{ currentPage }}
        <div class="card-list">

            <product-card v-for="product in data?.results" :product="product" :key="product.id"/>
        </div>
    </div>
<!--    <div class="container">-->
<!--        <div class="dropdown d-flex justify-content-end my-2">-->
<!--            <a-->
<!--                    class="btn btn-secondary dropdown-toggle"-->
<!--                    href="#"-->
<!--                    role="button"-->
<!--                    data-bs-toggle="dropdown"-->
<!--                    aria-expanded="false"-->
<!--            >-->
<!--                Sort by-->
<!--            </a>-->

<!--            <ul class="dropdown-menu">-->
<!--                <li>-->
<!--                    <RouterLink-->
<!--                            :to="{ name: 'products', query: { ...route.query, ordering: 'price' } }"-->
<!--                            class="dropdown-item"-->
<!--                    >-->
<!--                        Price asc-->
<!--                    </RouterLink>-->
<!--                </li>-->
<!--                <li>-->
<!--                    <RouterLink-->
<!--                            :to="{ name: 'products', query: { ...route.query, ordering: '-price' } }"-->
<!--                            class="dropdown-item"-->
<!--                    >-->
<!--                        Price desc-->
<!--                    </RouterLink>-->
<!--                </li>-->
<!--            </ul>-->
<!--        </div>-->
<!--        <div v-if="isLoaded" class="row row-cols-4 g-2">-->
<!--            <div-->
<!--                    class="card card-hover py-5 text-center container"-->
<!--                    style="width: 17%"-->
<!--                    v-for="product in products"-->
<!--                    :key="product.id"-->
<!--            >-->
<!--                <RouterLink :to="'products/' + product.id">-->
<!--                    <img :src="product.image" class="card-img-top" :alt="product.title"/>-->
<!--                </RouterLink>-->
<!--                <div class="card-body">-->
<!--                    <h5 class="card-title">{{ product.title }}</h5>-->
<!--                    <p class="card-text">{{ product.price }}</p>-->
<!--                    <button class="btn btn-primary" @click="cartMethods.addToCart(product)">-->
<!--                        Add to cart-->
<!--                    </button>-->
<!--                </div>-->
<!--            </div>-->
<!--            <nav class="py-4" aria-label="Page navigation example">-->
<!--                <ul class="pagination">-->
<!--                    <li class="page-item" v-for="i in pages" :key="i">-->
<!--                        <RouterLink-->
<!--                                :to="{ name: 'products', query: { ...route.query, page: i } }"-->
<!--                                class="page-link"-->
<!--                        >{{ i }}-->
<!--                        </RouterLink-->
<!--                        >-->
<!--                    </li>-->
<!--                </ul>-->
<!--            </nav>-->
<!--        </div>-->
<!--        <div v-else>-->
<!--            <p>Loading...</p>-->
<!--        </div>-->
<!--    </div>-->
</template>

<style scoped>
.card-hover:hover {
    box-shadow: 0 0 11px rgba(33, 33, 33, 0.2);
}

.card-list {
    display: flex;
    flex-direction: column;
    gap: 20px;
    flex-wrap: wrap;
    /*justify-content: space-between;*/
    align-content: center;
}
</style>
