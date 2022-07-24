<template>
  <div class="banner max-w-full h-80 bg-cover bg-no-repeat flex flex-col space-y-20 items-center justify-center sm:bg-center">
        <img class="w-32" src="/img/tmdb-logo.svg" alt="">
        <h1 class="text-6xl text-white font-bold  ">ReleaseWhen</h1>
        <div class="relative">
            <input v-model="movie" type="text" placeholder="Buscar por um filme..." class="w-96 h-8 py-5 pl-5 pr-12 rounded-3xl outline-none border-none focus:ring focus:ring-red-900 ">
            <button @click="search" class="absolute h-full p-2 right-0 bg-gradient-to-r from-red-300 to-yellow-200 rounded-3xl text-red-900 hover:text-black">Buscar</button>
        </div>
  </div>
</template>

<script>



export default {
    name: 'Header',
    data(){
        return {
           movie: ''
        }
    },
    methods: {
        search(){
            this.emitter.emit('search', this.movie)
        }
    }
}
</script>

<style scoped>
    .banner {
        background-image: url('/img/popcorn.webp');
    }

</style>