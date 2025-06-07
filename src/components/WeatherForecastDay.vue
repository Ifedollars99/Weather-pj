<script setup>
import { defineProps } from 'vue';

// Define the props expected by this component
const props = defineProps({
  day: {
    type: Object,
    required: true
  }
});
</script>

<template> 
  <div class="mb-2 flex items-center justify-between">
    <table class="w-full">
      <tr>
        <!-- Day of the week -->
        <td class="w-1/3">
          {{ new Date(props.day?.date).toLocaleDateString('en-us', { weekday: 'long' }) }}
        </td>

        <!-- Icon -->
        <td class="w-1/3">
          <!-- Safely access condition.icon with fallback -->
          <img :src="props.day?.day?.condition?.icon || '/path/to/default/icon.png'" alt="icon" width="30" class="mx-auto">
        </td>

        <!-- Temperature (Max/Min) -->
         
        <td class="w-1/3 text-right">
          {{ Math.round(props.day?.day?.maxtemp_c || 0) }} / {{ Math.round(props.day?.day?.mintemp_c || 0) }}
        </td>
      </tr>
    </table>
  </div>
</template>