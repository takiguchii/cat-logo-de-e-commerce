<template>
    <div
        class="bg-white rounded-xl shadow-md overflow-hidden transition-transform hover:-translate-y-1 hover:shadow-xl">
        <div class="aspect-square">
            <img :src="categoryImage" :alt="categoryName" class="w-full h-full object-cover">
        </div>
        <div class="p-4">
            <h3 class="text-lg font-semibold text-gray-800 text-center capitalize">{{ categoryName }}</h3>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const props = defineProps({
    categoryName: {
        type: String,
        required: true
    }
});

const categoryImage = ref('');

onMounted(async () => {
    try {
        const response = await fetch(`https://dummyjson.com/products/category/${props.categoryName}`);
        const data = await response.json();
        if (data.products && data.products.length > 0) {
            categoryImage.value = data.products[0].thumbnail;
        }
    } catch (error) {
        console.error('Error fetching category image:', error);
        categoryImage.value = 'https://placehold.co/400x400?text=No+Image';
    }
});
</script>
