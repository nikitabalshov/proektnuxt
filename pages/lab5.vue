<template>
    <main>
        <NuxtLink to="/" class="text-2xl">Go to previous lab</NuxtLink>
        <label for="select">Pick up your Primarch</label> 
        <select id="select" v-model="selectus">
            <option value="Emperor">Emperor</option>
            <option value="Giliman">Giliman</option>
            <option value="Horus">Horus</option>
            <option value="Ferrus">Ferrus</option>
        </select>
        <div class="flex justify-center" v-if="selectus === 'Emperor'">
            <Emperor />
        </div>
        <div class="flex justify-center" v-else-if="selectus === 'Giliman'">
            <Giliman />
        </div>
        <div class="flex justify-center" v-else-if="selectus === 'Ferrus'">
            <Ferrus />
        </div>
        <div class="flex justify-center" v-else-if="selectus === 'Horus'">
            <Horus />
        </div>
        <div class="flex justify-center">
            <calculator />
        </div>
        <div class="flex justify-center">
            <krestikinoliki />
        </div>
    </main>
</template>

<script setup lang="ts">
import { ref,computed } from 'vue';


import Emperor from '~/components/Emperor.vue';
import Giliman from '~/components/Giliman.vue';
import Ferrus from '~/components/Ferrus.vue';
import Horus from '~/components/Horus.vue';
import calculator from '~/components/calculator.vue';
import krestikinoliki from '~/components/krestikinoliki.vue';

const selectus = ref('Emperor');
</script>