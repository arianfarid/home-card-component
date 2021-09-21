<template>
  <div v-for="house in houseData" v-bind:key="house.id">
    <HouseCard :data="house" :realtor="returnRealtor(house.realtor_id)" :favorite="returnFavorite(house.id)" @toggled-favorite="toggleFavorite($event)" />
  </div>
</template>

<script>
import HouseCard from './components/HouseCard.vue'
import homeData from './assets/homeData.json'
import realtorData from './assets/realtorData.json'
import {ref} from 'vue'
export default {
  name: 'App',
  components: {
    HouseCard
  }, setup () {
    // House and realtor logic
    const houseData = homeData;
    const realtors = realtorData;
    const returnRealtor = (realtor_id) => {
      return realtors[realtors.findIndex(realtor => realtor.id === realtor_id)]
    }

    // Favorites logic
    const favorites = ref([])
    const toggleFavorite = (event) => {
      if (!favorites.value.includes(event.id)) {
        favorites.value.push(event.id)
      } else if (favorites.value.includes(event.id)) {
        favorites.value = favorites.value.filter(f => f !== event.id)
      }
      return 
    }
    const returnFavorite = (id) => {
      return favorites.value.includes(id)
    }

    return {houseData, realtors, returnFavorite, returnRealtor, toggleFavorite}
  }
}
</script>
