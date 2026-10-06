<script setup>
import { onMounted, ref, reactive, watch } from 'vue'
import axios from 'axios'

import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'

const items = ref([]);

const filters = reactive({
  sortBy: 'title',
  searchQuery: ''
})

const onChangeSelect = event => {
  filters.sortBy = event.target.value;
}

const onChangeSearchInput = event => {
  filters.searchQuery = event.target.value;
}

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy
    };

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`;
    }

    const { data } = await axios.get(`https://7b9204c891dd1ad5.mokky.dev/items`, {
      params
    });

    items.value = data.map(obj => ({
      ...obj,
      isFavorite: false,
      isAdded: false,
    }))

  } catch (err) {
    console.log(err);
  }
}

onMounted(async () => {
  await fetchItems();
  await fetchFavorites();
});
watch(filters, fetchItems);


const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get(`https://7b9204c891dd1ad5.mokky.dev/favorites`);
    items.value = items.value.map(item => {
      const favorite = favorites.find(favorite => favorite.parentId === item.id)

      if (!favorite) {
        return item;
      }
      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id
      }
    })

    console.log(items.value)
  } catch (err) {
    console.log(err);
  }
}

</script>


<template>
  <!-- <Drawer /> -->

  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">

    <Header />

    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>

        <div class="flex gap-4">
          <select @change="onChangeSelect" class="py-2 px-3 border rounded-md outline-none" name="" id="">
            <option value="name">По названию</option>
            <option value="price">Сначала дешевые</option>
            <option value="-price">Сначала дорогие</option>
          </select>

          <div class="relative">
            <img class="absolute left-3 top-3" src="/search.svg" alt="search">
            <input @input="onChangeSearchInput"
              class="border rounded-md border-gray-200 py-2 pl-10 pr-4 outline-none transition focus:border-gray-400"
              type="text" placeholder="Поиск" />
          </div>
        </div>
      </div>

      <div class="mt-6">
        <CardList :items="items" />
      </div>
    </div>

  </div>
</template>


<style scoped lans="sass"></style>
