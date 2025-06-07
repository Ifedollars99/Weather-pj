<script setup >
defineProps({
    place: Object
})
</script>

<template>
    <div class="absolute bg-white/80 backdrop-blur-sm text-slate-500 inset-0 bottom-0 rounded-t-lg p-8" >
        <!-- Close button -->
         <div class="flex justify-end mb-10 " >
            <button @click="$emit('close-info')" class="p-1" >
              <i class="bi bi-x-octagon text-black text-2xl font-bold top-10"></i>
            </button>
         </div>

         <div class="flex items-center justify-between gap-6 mb-20" >
            <!-- Wind speed -->
             <div class="text-center flex-1" >
                <i class="fa-solid fa-wind text-2xl" ></i>
                <p class="text-xl font-bold" >{{ place.current.wind_kph }} km/hr </p>
                <p>wind</p>
             </div>

             <!-- Humidity level -->
              <div class="text-center flex-1" >
                <i class="fa-solid fa-droplet mb text-2xl" ></i>
                <p class="text-xl font-bold" >{{ place.current.humidity }}</p>
                <p>humidity</p>
              </div>

              <!-- Precipitation -->
               <div class="text-center flex-1" >
                <i class="fa-solid fa-umbrella mb text-2xl" ></i>
                <p class="text-xl font-bold " >{{place.current.precip_mm}} mm</p>
                <p>precipitation</p>
               </div>

         <div class="flex items-center justify-between gap-6 mb-10" >
            <!-- Wind direction -->
             <div class="text-center flex-1" >
                <i class="fa-solid fa-fan mb text-2xl" ></i>
                    <p class="text-xl font-bold" >{{place.current.wind_dir}}</p>
                <p>direction</p>
             </div>
             <!-- Feels like -->
              <div class="text-center flex-1" >
                <i class="fa-solid fa-temperature-half mb text-2xl" ></i>
                <p class="text-xl font-bold" >{{Math.round(place.current.feelslike_c)}}</p>
                <p>Feels</p>
              </div>
         </div>
         <!-- UV -->
          <div class="text-center flex-1" >
            <i class="fa-solid fa-sun mb text-2xl" ></i>
            <p class="text-2xl font-bold" >{{place.current.uv}}</p>
            <p>UV index</p>
          </div>
         <!-- last update and delete -->
          <div class="flex justify-evenly items-center" ></div>
          <h3 class="text-slate-900/50" >lastupdate: {{place.current.last_updated}} </h3>
          <button @click="$emit('remove-place')" >
           
          </button>
    </div>
    <div>
      <p class="text-black" >Delete weather box</p>
   <i class="bi bi-trash3-fill text-black font-bold text-2xl"></i>
    </div>
  
    </div>
</template>