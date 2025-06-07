<script setup>
import BorderLine from './BorderLine.vue';
import WeatherForecastDay from './WeatherForecastDay.vue';
import WeatherInfo from './WeatherInfo.vue';
import { ref } from 'vue';

defineProps({
    place: Object
})

const emit = defineEmits(['delete-place'])

const showDetail = ref(false)

const removePlace = (placeName) => {
    emit('delete-place', placeName)
    showDetail.value = false
}
</script>

<template>
    <div class="p-2">
        <div class="text-white p-10 rounded-lg shadow-lg gap-6 mb-6 relative overflow-hidden bg-blue-500">
            <!-- Location & time -->
            <div class="mb-2 flex justify-between items-center">
                <div class="flex items-center justify-center gap-2">
                    <i class="bi bi-geo-alt-fill"></i>
                    <h1 class="text-3xl">{{ place.location.name }}</h1>
                </div>
                <div class="flex items-center justify-center gap-2">
                    <i class="bi bi-clock"></i>
                    <h1 class="text-3xl">{{ place.location.localtime }}</h1>
                </div>

            </div>

            <!-- current weather -->
            <div class="text-center flex-1">
                <img :src="place.current.condition.icon" alt="item" width="200" class="mx-auto -mb-10" />
                <h3 class="text-3xl mb-2 -mr-4">{{ Math.round(place.current.temp_c) }}&deg;</h3>
                <p class="text-2xl">{{ place.current.condition.text }}</p>
            </div>

            <BorderLine />

            <!-- forecast -->
            <div v-for="(day, idx) in place.forecast.forecastday" :key="idx">
                <WeatherForecastDay :day="day" />
            </div>

            <!-- Info -->
            <div v-show="showDetail">
                <WeatherInfo :place="place" @close-info="showDetail = false"
                    @remove-place="removePlace(place.location.name)" />
            </div>


            <!-- forecast btn -->
            <div class="flex justify-end items-center gap-3 mt-10">
                <button @click="showDetail = true">More <i class="bi bi-arrow-right text-sm -mb-px"></i></button>
            </div>
        </div>
    </div>
</template>