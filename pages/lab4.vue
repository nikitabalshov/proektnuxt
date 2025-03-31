<template class="overflow-hidden">
  <main 
  :class="selectedCharacter ? 'flex flex-col items-center justify-center bg-cover bg-center  p-0' : 'flex flex-col items-center justify-center w-screen h-screen bg-gray-100'"
  :style="selectedCharacter ? { backgroundImage: `url(${selectedCharacter.image})`, backgroundSize: 'contain', backgroundPosition: 'center', backgroundRepeat: 'no-repeat' } : {}"
  class="w-screen h-[790px] relative overflow-hidden">
    <div class="absolute inset-0 pointer-events-none">
      <div class="absolute top-0 left-0 w-1/2 h-full bg-gradient-to-r from-black/100 to-transparent"></div>
      <div class="absolute top-0 right-0 w-1/2 h-full bg-gradient-to-l from-black/100 to-transparent"></div>
    </div>
    <h1
      v-if="selectedCharacter"
      class="absolute top-4 text-3xl font-bold text-white text-center w-full z-10"
    >
      {{ selectedCharacter.name }}
    </h1>
  <div
      v-if="selectedCharacter"
      class="absolute left-4 top-1/3 p-4 color-white rounded-lg shadow-lg max-w-sm z-10"
      style="background: radial-gradient(circle, rgba(0, 0, 0, 0.8) 0%, rgba(0, 0, 0, 0) 100%);"
    >
      <h2 class="text-xl text-white font-bold mb-2">Description</h2>
      <p class="text-sm text-white">{{ selectedCharacter.Description }}</p>
    </div>

    <div class="carousel-container fixed bottom-0 border border-yellow-500 left-0 w-full bg-brown-200 py-4 bg-[#86400ee7]">
      <div class="carousel flex overflow-x-auto gap-4 px-4">
        <div
          v-for="(character, index) in characters"
          :key="index"
          :class="['carousel-item flex flex-col items-center p-4 border rounded-lg bg-gray-400 cursor-pointer', selectedCharacter === character ? 'bg-yellow-300 border-yellow-500' : 'hover:bg-yellow-200']"
          @click="selectCharacter(character)"
        >
          <img :src="character.icon" alt="character" class="w-24 h-24 mb-2 rounded-full" />
          <p class="text-sm font-semibold">{{ character.name }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup lang="ts">
import { reactive, ref } from 'vue';
interface Character {
  name: string;
  image: string;
  icon: string;
  Description: string;
}
const defaultCharacter: Character = {
  name: 'Emperor',
  image: '/Default/Imperator.jpg',
  icon: null,
  Description: 'The Emperor of Mankind is the immortal Perpetual who serves as the ruling monarch',
};


const characters = reactive<Character[]>([
  {name:'Ferrus', icon: '/Ferrus/Ferrus.webp',image: '/Ferrus/Ferrus_Back.webp', Description: 'Ferrus Manus, known as the Gorgon, was the loyal Primarch of the Iron Hands Legion. He was one of the Emperor of Mankind\'s 20 genetically-engineered sons, and his saga is one of the most tragic in the history'},
  {name:'Fulgrim', icon: '/Fulgrim/fulgrim.webp',image:'/Fulgrim/Fulgrim_Back.webp',Description: 'Fulgrim, known in his early life as the Phoenician, is the Primarch of the Emperor\'s Children, a loyalist Space Marine Legion of superhuman warriors raised by the Emperor of Mankind to unite the galaxy in the late 30th Millennium'},
  {name:'Giliman', icon: '/Giliman/Giliman.webp',image:'/Giliman/Giliman_Back.webp',Description: 'Roboute Guilliman, known as The Avenging Son, is the Primarch of the Ultramarines Chapter of Space Marines. He is a master strategist and tactician, and his leadership has saved the Imperium from destruction on multiple occasions'},
  {name:'Horus', icon: '/Horus/Horus.webp',image:'/Horus/Horus_Back.webp',Description: 'Horus Lupercal, also known more simply as "Horus," was one of the 20 genetically-engineered Primarchs created by the Emperor of Mankind from the foundation of His own DNA before the start of the Great Crusade to lead the armies of the newborn'},
  {name:'Jaghatai', icon: '/Jaghatai/Jaghatai.webp',image:'/Jaghatai/Jaghatai_Back.webp',Description: 'Jaghatai Khan, known as the Great Khan and the Warhawk, was the Primarch of the White Scars Space Marine Legion. He was known for his lightning-fast attacks and his fierce loyalty to the Emperor of Mankind'},
  {name:'Konrad', icon: '/Konrad/Konrad.webp',image:'/Konrad/Konrad_Back.webp',Description: 'Konrad Curze, also known as Night Haunter, was the Primarch of the Night Lords Space Marine Legion. He was a brutal and sadistic figure who inspired fear and terror in his enemies and his own people alike'},
  {name:'Leman', icon: '/Leman/Leman.webp',image:'/Leman/Leman_Back.webp',Description: 'Leman Russ, known also as the Wolf King and the Great Wolf during his lifetime, is the currently missing Primarch of the Space Wolves Chapter of Space Marines. He is known for his ferocity in battle and his loyalty to the Emperor of Mankind'},
  {name:'Lev', icon: '/Lev/Lion.webp',image:'/Lev/Lion_Back.webp',Description: 'Lion El\'Jonson, known also as the Lion and the Wolf of Caliban, is the Primarch of the Dark Angels Space Marine Chapter and one of the greatest heroes of the imperium'},
  {name:'Lorgar', icon: '/Lorgar/Lorgar.webp',image:'/Lorgar/Lorgar_Back.webp',Description: 'Lorgar Aurelian, also known as Lorgar, the Urizen, the Golden One and the Bearer of the Word, is the Primarch of the Word Bearers Space Marine Legion. He was the first of the Emperor of Mankind\'s genetically-engineered sons to turn to Chaos'},
  {name:'Magnus', icon: '/Magnus/Magnus.webp',image:'/Magnus/Magnus_Back.webp',Description: 'Magnus the Red, known also as the Crimson King and the Sorcerer King, is the Primarch of the Thousand Sons Space Marine Legion. He was one of the Emperor of Mankind\'s 20 genetically-engineered sons, and his psychic abilities were unmatched by any other Primarch'},
  {name:'Mortarion', icon: '/Mortarion/Mortarion.webp',image:'/Mortarion/Mortarion_Back.webp',Description: 'Mortarion, also known as the Death Lord, the Prince of Decay and the Pale King, is the Primarch of the Death Guard Space Marine Legion. He was one of the Emperor of Mankind\'s 20 genetically-engineered sons, and his saga is one of the most tragic in the history of the Imperium'},
  {name:'Perturado', icon: '/Perturado/Perturado.webp',image:'/Perturado/Perturado_Back.webp',Description: 'Perturabo, also known as the Lord of Iron and the Breaker of Cities, is the Primarch of the Iron Warriors Space Marine Legion. He was one of the Emperor of Mankind\'s 20 genetically-engineered sons, and his saga is one of the most tragic in the history of the Imperium'},
  {name:'Rogal', icon: '/Rogal/Rogal.webp',image:'/Rogal/Rogal_Back.webp',Description: 'Rogal Dorn, known also as the Praetorian of Terra, the Vigilant, and the Unyielding One, is the Primarch of the Imperial Fists Space Marine Legion. He was one of the Emperor of Mankind\'s 20 genetically-engineered sons, and his saga is one of the most tragic in the history of the Imperium'},
  {name:'Sanguinius', icon: '/Sanguinius/Sanguinius.webp',image:'/Sanguinius/Sanguinius_Back.webp',Description: 'Sanguinius, known as the Great Angel and the Brightest One, is the Primarch of the Blood Angels Space Marine Legion.'},
  {name:'Vulcan', icon: '/Vulcan/Vulcan.webp',image:'/Vulcan/Vulcan_Back.webp',Description: 'Vulkan, known also as the Lord of Drakes and the Son of the Ember, is the Primarch of the Salamanders Space Marine Legion. He was one of the Emperor of Mankind\'s 20 genetically-engineered sons, and his saga is one of the most tragic in the history of the Imperium'},
  {name:'Corax', icon: '/Corax/Corax.webp',image:'/Corax/Corax_Back.webp',Description: 'Corvus Corax, also known as the Lord of Shadows and the Deliverer, is the Primarch of the Raven Guard Space Marine Legion. He was one of the Emperor of Mankind\'s 20 genetically-engineered sons, and his saga is one of the most tragic in the history of the Imperium'},
  {name:'Angron',icon:'/Angron/Angron.webp',image:'/Angron/Angron_Back.webp',Description:'Angron, also known as the Red Angel, the Lord of the Red Sands, and the Master of the Twelfth, is the Primarch of the World Eaters Space Marine Legion. He was one of the Emperor of Mankind\'s 20 genetically-engineered sons, and his saga is one of the most tragic in the history of the Imperium'},
  {name:'Alpharius', icon: '/Alpharius/Alpharius.webp',image:'/Alpharius/Alpharius_Back.webp',Description: 'Alpharius, also known as the Last Primarch and the Lord of Serpents, is the Primarch of the Alpha Legion Space Marine Legion. He was one of the Emperor of Mankind\'s 20 genetically-engineered sons, and his saga is one of the most tragic in the history of the Imperium'}
]);


const selectedCharacter = ref<Character | null>(defaultCharacter);
;


function selectCharacter(character: Character) {
  selectedCharacter.value = character;
}
</script>

<style scoped>

main {
  background-size: cover;
  background-position: center;
  transition: background-image 0.5s ease-in-out;
  max-height: 920px;
}


.carousel-container {
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 -2px 5px rgba(0, 0, 0,1);
}

.bg-black {
  background-color: black;
}

.opacity-50 {
  opacity: 0.5;
}

.transition-opacity {
  transition: opacity 0.5s ease-in-out;
}
.carousel {
  display: flex;
  overflow-x: auto;
  scroll-behavior: smooth;
}

.carousel-item {
  flex: 0 0 auto;
  width: 100px;
  text-align: center;
}

.carousel-item img {
  transition: transform 0.3s ease;
}

.carousel-item:hover img {
  transform: scale(1.1); 
}
</style>