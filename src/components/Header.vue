<template>
    <header class="flex justify-between border-b border-slate-100 border-color px-8 py-10">
        <div class="flex items-center gap-4">
            <img src="/logo.png" alt="Logo" class="w-10">
            <div>
                <h2 class="text-xl font-bold uppercase">Vue Sneakers</h2>
                <p class="text-slate-400">Магазин лучших кроссовок</p>
            </div>
        </div>

        <ul class="flex items-center gap-10">
            <li class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black duration-300">
                <img src="/cart.svg" alt="cart">
                <b class="">1205 руб</b>
            </li>
            <li class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black duration-300">
                <img src="/heart.svg" alt="heart">
                <span class="">Закладки</span>
            </li>
            <li class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black duration-300">
                <img src="/profile.svg" alt="profile">
                <span class="">Профиль</span>
            </li>
        </ul>
    </header>
</template>