<script setup>
import Card from './Card.vue'

defineProps({
    items: Array,
})

const onClickAdd = () => {
    isAdded = !isAdded
}
</script>


<template>
    <div class="grid grid-cols-4 gap-5">
        <Card v-for="item in items" v-key="item.id" :imageUrl="item.imageUrl" :title="item.title" :price="item.price"
            :isAdded="false" :isFavorite="true" :onClickAdd="onClickAdd" />
    </div>
</template>