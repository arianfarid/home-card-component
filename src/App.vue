<template>
  <div v-for="house in houseData" v-bind:key="house.id">
    <HouseCard :data="house" :realtor="returnRealtor(house.realtor_id)" />
  </div>
</template>

<script>
import HouseCard from './components/HouseCard.vue'
import homeData from './assets/homeData.json'
import realtorData from './assets/realtorData.json'
export default {
  name: 'App',
  components: {
    HouseCard
  }, setup () {
    const houseData = homeData;
    const realtors = realtorData;
    const returnRealtor = (realtor_id) => {
      return realtors[realtors.findIndex(realtor => realtor.id === realtor_id)]
    }
    return {houseData, realtors, returnRealtor}
  }
}
</script>
