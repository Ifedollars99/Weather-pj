<template>
<main>
  <!-- DashBoard -->
   <div class="bg-white w-full h-28 md:h-20 shadow-md flex flex-col md:flex-row items-center justify-between p-4" >
    <div class="flex flex-row gap-2" >
      <i class="bi bi-brightness-high text-blue-500 text-2xl"></i>
      <h1 class="text-black text-xl font-bold mt-1" >Weather DashBoard</h1>
    </div>
  <!-- Date -->
   <div class="flex flex-row gap-2" >
    <h1 class="text-sm mt-0.5" >Today's Date:</h1>
    {{ 
      new Date().toLocaleDateString('en-us', {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      })
       }}
   </div>
</div>
    <!-- Search -->
     <div>
      <SearchField @place-data= "addPlace"/>
     </div>

     <!-- Weather Cards -->
      <div class="grid grid-cols-2 gap-4" >
        <div v-for="(place, idx) in places" :key="idx">
          
       <WeatherCard :place="place" @delete-place="deletePlace"/>
      </div>
      </div>
</main>

  <router-view class="text-transparent" ></router-view>
</template>

<script setup >
import { ref } from 'vue';
import SearchField from './components/SearchField.vue';
import WeatherCard from './components/WeatherCard.vue';

const places = ref([])

const addPlace = (data) => {
  places.value.push(data)
}

const deletePlace = (name) => {
  places.value = places.value.filter(p => p.location.name !== name)
}

</script>

<style scoped>
 
</style> 

 