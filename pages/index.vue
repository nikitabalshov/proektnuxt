<template>
    <main class="flex flex-col min-h-screen">
      <!-- Первый блок -->
      <div :class="{
        'flex-1 flex bg-red-400': parseFloat(hum) > 75 && parseFloat(hum) < 78,
        'flex-1 flex bg-[#08f3f3]': parseFloat(hum) >= 78,
        'flex-1 flex': true
      }">
        <div class="flex flex-col items-center gap-2 m-auto">
          <img src="/Default/Imperator.jpg" alt="Emperor" class="w-24 h-32 rounded-sm">
          <p>T in degree: {{ temp || "loading..." }}</p>
          <p>Hum in %: {{ hum || "loading..." }}</p>
          <p>Wind speed in m/s: {{ wind || "loading..." }}</p>
        </div>
      </div>
  
      <!-- Второй блок -->
      <div class="flex-1 flex">
        <div class="flex flex-col items-center gap-2 m-auto">
          <img src="/Default/Imperator.jpg" alt="Emperor" class="w-24 h-32 rounded-sm">
          <p>T in degree: {{ temp1 || "loading..." }}</p>
          <p>Hum in %: {{ hum1 || "loading..." }}</p>
          <p>Wind speed in m/s: {{ wind1 || "loading..." }}</p>
        </div>
      </div>
  
      <!-- Третий и четвертый блоки -->
      <div class="flex-1 flex">
        <div :class="{
          'flex-1 flex bg-red-400': parseFloat(hum2) > 75 && parseFloat(hum2) < 78,
          'flex-1 flex bg-[#08f3f3]': parseFloat(hum2) >= 78,
          'flex-1 flex': true
        }">
          <div class="flex flex-col items-center gap-2 m-auto">
            <img src="/Default/Imperator.jpg" alt="Emperor" class="w-24 h-32 rounded-sm">
            <p>T in degree: {{ temp2 || "loading..." }}</p>
            <p>Hum in %: {{ hum2 || "loading..." }}</p>
            <p>Wind speed in m/s: {{ wind2 || "loading..." }}</p>
          </div>
        </div>
  
        <div class="flex-1 flex">
          <div class="flex flex-col items-center gap-2 m-auto">
            <img src="/Default/Imperator.jpg" alt="Emperor" class="w-24 h-32 rounded-sm">
            <p>T in degree: {{ temp3 || "loading..." }}</p>
            <p>Hum in %: {{ hum3 || "loading..." }}</p>
            <p>Wind speed in m/s: {{ wind3 || "loading..." }}</p>
          </div>
        </div>
      </div>
    </main>
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  
  const temp = ref<string>('');
  const hum = ref<string>('');
  const wind = ref<string>('');
  
  const temp1 = ref<string>('');
  const hum1 = ref<string>('');
  const wind1 = ref<string>('');
  
  const temp2 = ref<string>('');
  const hum2 = ref<string>('');
  const wind2 = ref<string>('');
  
  const temp3 = ref<string>('');
  const hum3 = ref<string>('');
  const wind3 = ref<string>('');
  
  const fetching = async (): Promise<void> => {
    const response = await axios.get('https://api.open-meteo.com/v1/forecast?latitude=55.8833&longitude=13.3167&current=temperature_2m,relative_humidity_2m,wind_speed_10m');
    temp.value = response.data.current.temperature_2m;
    hum.value = response.data.current.relative_humidity_2m;
    wind.value = response.data.current.wind_speed_10m;
  
    const response1 = await axios.get('https://api.open-meteo.com/v1/forecast?latitude=43.2979&longitude=13.4529&hourly=temperature_2m,wind_speed_10m,relative_humidity_2m');
    temp1.value = response1.data.temperature_2m;
    hum1.value = response1.data.relative_humidity_2m;
    wind1.value = response1.data.wind_speed_10m;

    const response2 = await axios.get('https://api.open-meteo.com/v1/forecast?latitude=42.2272&longitude=-111.401&hourly=temperature_2m,wind_speed_10m,relative_humidity_2m');
    temp2.value = response2.data.temperature_2m;
    hum2.value = response2.data.relative_humidity_2m;
    wind2.value = response2.data.wind_speed_10m;
  
    const response3 = await axios.get('https://api.open-meteo.com/v1/forecast?latitude=54.8667&longitude=69.15&hourly=temperature_2m,wind_speed_10m,relative_humidity_2m');
    temp3.value = response3.data.temperature_2m;
    hum3.value = response3.data.relative_humidity_2m;
    wind3.value = response3.data.wind_speed_10m;
  };
  
  onMounted(() => {
    fetching();
    setInterval(fetching, 5000);
  });
  </script>
