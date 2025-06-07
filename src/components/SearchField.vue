<script setup>
import { reactive } from 'vue';

const emit = defineEmits(['place-data'])

const searchTerm = reactive({
    query: '',
    timeout: null,
    results: null,
})

const handleSearch = () => {
    clearTimeout(searchTerm.timeout)
    searchTerm.timeout = setTimeout(async () => {
        if (searchTerm.query !== '') {
            const res = await fetch(
                `http://api.weatherapi.com/v1/search.json?key=5c5dc524abe34ee9a38103400242912&q=${searchTerm.query}`
            )

            const data = await res.json()
            searchTerm.results = data
        } else {
            searchTerm.results = null
        }
    }, 500)
}

const getWeather = async (id) => {
    const res = await fetch(
        `https://api.weatherapi.com/v1/search.json?key=5c5dc524abe34ee9a38103400242912&q=${searchTerm.query}`
    )

    const data = await res.json()

    emit('place-data', data)

    searchTerm.query = ''
    searchTerm.results = null
}
</script>

<template>
    <div>
        <!-- Search field -->
        <form class="mt-5 p-2">
            <div class="flex flex-row gap-1">
                <i class="bi bi-geo-alt text-lg text-gray-500"></i>
                <h1 class="text-lg text-gray-500">Location</h1>
            </div>
            <div class="bg-white border border-indigo-600/30 rounded-lg shadow-lg flex items-center mt-2">
                <i class="bi bi-search p-2 font-bold text-indigo-600"></i>
                <input type="text" placeholder="Search for a place"
                    class="rounded-r-lg p-2 border-0 outline-0 focus:ring-2 focus:ring-indigo-600 ring-inset w-"
                    v-model="searchTerm.query" @input="handleSearch" />
            </div>
        </form>
        <!-- search suggestion -->
        <div class="p-2">
            <div class="bg-white my-2 rounded-lg shadow-lg p-3 ">
                <div v-if="searchTerm.results !== null">
                    <div v-for="place in searchTerm.results" :key="place.id">
                        <button @click="getWeather(place.id)"
                            class="px-3 my-2 hover:text-indigo-600 hover:font-bold w-full text-left">
                            {{ place.name }}, {{ place.region }}, {{ place.country }}
                        </button>
                    </div>
                </div>
            </div>


        </div>
    </div>
</template>