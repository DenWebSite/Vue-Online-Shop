<script setup>

defineProps({
    imageUrl: String,
    title: String,
    price: Number,

    isFavorite: Boolean,
    isAdded: Boolean,

    onClickAdd: Function,
    onClickFavorite: Function,
})

</script>

<template>
    <div
        class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl">
        <img class="absolute top-8 left-8 shadow rounded-md" :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'" alt="Like button">
        <img :src="imageUrl" alt="Sneaker" @click="onClickFavorite">
        <p class="mt-2">{{ title }}</p>

        <div class="flex justify-between mt-5">
            <div class="flex flex-col">
                <span class="text-slate-400 uppercase">Цена:</span>
                <b>{{ price }} руб.</b>
            </div>

            <img :src="!isAdded ? '/plus.svg' : '/checked.svg'" alt="Plus" @click="onClickAdd">
        </div>
    </div>
</template>
