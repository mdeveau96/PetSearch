<script setup lang="ts">
import { ref, onMounted } from "vue";
import Card from "primevue/card";
import { ProductService } from '@/service/ProductService';
import PostCard from "./PostCard.vue";

onMounted(() => {
    ProductService.getProductsSmall().then((data: string | any[]) => (products.value = data.slice(0, data.length)));
});

const products = ref();
const sortKey = ref();
const sortOrder = ref();
const sortField = ref();
const sortOptions = ref([
    {label: 'Price High to Low', value: '!price'},
    {label: 'Price Low to High', value: 'price'},
]);
const onSortChange = (event: { value: { value: any; }; }) => {
    const value = event.value.value;
    const sortValue = event.value;

    if (value.indexOf('!') === 0) {
        sortOrder.value = -1;
        sortField.value = value.substring(1, value.length);
        sortKey.value = sortValue;
    }
    else {
        sortOrder.value = 1;
        sortField.value = value;
        sortKey.value = sortValue;
    }
};

</script>


<template>
    <div class="grid grid-cols-1 gap-4">
        <Card v-for="post in products" :key="post.id" class="min-w-[680px]">
            <template #content>
                <!-- {{ post.description }} -->
                  <PostCard/>
            </template>
        </Card> 
    </div>
</template>
