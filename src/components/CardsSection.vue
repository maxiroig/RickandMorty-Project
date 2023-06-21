<script setup>
import { onMounted, ref } from 'vue';
import axios from 'axios'

const people = [
    {
        name: 'Leonard Krasner',
        role: 'Senior Designer',
        imageUrl:
            'https://images.unsplash.com/photo-1519345182560-3f2917c472ef?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=8&w=1024&h=1024&q=80',
        twitterUrl: '#',
        linkedinUrl: '#',
    },
    // More people...
]
const characters = ref([])

const setResult = (response) => {
    characters.value = response
    console.log("c", characters.value);

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
            <ul role="list"
                class="mx-auto mt-20 grid max-w-2xl grid-cols-1 gap-6 sm:grid-cols-2 lg:mx-0 lg:max-w-none lg:grid-cols-3 lg:gap-8">
                <li v-for="(character) in characters" :key="character.name" class="rounded-2xl bg-gray-800 px-8 py-10">
                    <img class="mx-auto h-48 w-48 rounded-full md:h-56 md:w-56" :src="character.image" :alt="character.name" />
                    <h3 class="mt-6 text-base font-semibold leading-7 tracking-tight text-white hover:text-orange-500 hover:cursor-pointer">{{ character.name }}</h3>
                    <p class="text-sm leading-6 text-gray-400">{{ character.species }} - {{ character.status }}</p>
                    <p class="text-sm leading-6 text-gray-400">Gender: <span class="text-white">{{ character.gender }}</span></p>
                    <p class="text-sm leading-6 text-gray-400">Last know location: <span class="text-white">{{ character.location.name }}</span></p>
                </li>
            </ul>
        </div>
    </div>
</template>