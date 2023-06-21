<script setup>
import { onMounted, ref } from 'vue';


import axios from 'axios'

const characters = ref([])
const shortedCharacters = ref([])
const gender = ref("")

const setResult = (response) => {
    characters.value = response
    shortedCharacters.value = characters.value.slice(0, 6)
    console.log("characters", shortedCharacters.value);
}
onMounted(() => {
    axios
        .get('https://rickandmortyapi.com/api/character')
        .then(response => setResult(response.data.results))
})
</script>
<template>
    <div class="bg-gray-900 py-24 sm:py-32">
        <div class="mx-auto max-w-7xl px-6 text-center lg:px-8">
            <div>
                <label for="gender">Select Gender</label>
                <select
                v-model="gender"
                name="gender" id="gender">
                    <option value="male">Male</option>
                    <option value="female">Female</option>
                </select>
            </div>
            <input type="text" class="text-black">
            <ul role="list"
                class="mx-auto mt-20 grid max-w-2xl grid-cols-1 gap-6 sm:grid-cols-2 lg:mx-0 lg:max-w-none lg:grid-cols-3 lg:gap-8">
                <li 
                v-for="(character) in shortedCharacters" 
                :key="character.name" 
                class="rounded-2xl bg-gray-800 px-8 py-10">
                        <img class="mx-auto h-48 w-48 rounded-full md:h-56 md:w-56" :src="character.image" :alt="character.name" />
                        <h3 class="mt-6 text-base font-semibold leading-7 tracking-tight text-pink-800 hover:text-orange-500 hover:cursor-pointer">
                            {{ character.name }}
                        </h3>
                        <p class="text-sm leading-6 text-white-400">
                            <span :class="character.status === 'Alive' ? 'green-dot' : 'red-dot'"/>
                            {{ character.species }} - {{ character.status }}
                        </p>
                        <p class="text-sm leading-6 text-gray-400">Gender: <span class="text-white">{{ character.gender }}</span></p>
                        <p class="text-sm leading-6 text-gray-400">Last know location: <span class="text-white">{{ character.location.name }}</span></p>    
                </li>
            </ul>
        </div>
    </div>
</template>

<style>

.green-dot {
        height: 8px;
        width: 8px;
        background-color: green;
        border-radius: 50%;
        display: inline-block;
}
.red-dot {
        height: 8px;
        width: 8px;
        background-color: red;
        border-radius: 50%;
        display: inline-block;
}
</style>