<template>
  <div class="movie rounded-t-3xl p-2 ">
        <div class=" rounded-3xl h-64 mr-5">
            <img class="rounded-3xl" :src="img_url" alt="">
        </div>
        <div>
            <p class="text-sm font-bold">{{title}}</p>
            <template v-if="Number(days_to_release) > 0">
                <p class="text-sm font-normal italic mt-2">{{release_date}}</p>
                <p class="text-sm font-normal italic mt-2">Faltam: {{days_to_release}} dias para o lançamento</p>
            </template>
            
            <p class="text-sm font-normal italic mt-2" v-else-if="Number(days_to_release) == 0">Estreia Hoje</p>
            <p v-else class="text-sm font-normal italic mt-2">Estreiou em {{release_date}}</p>
        </div>
  </div>
</template>

<script>
export default {
    name: 'Movie',
    props: {
        img_url: {
            type: String,
        },
        title: {
            type: String
        },
        release_date: {
            type: String
        },
        days_to_release: {
            type: String
        }
    },
    // computed: {
    //     formatDateTime(){
    //         return this.release_time.toLocaleDateString()
    //     }
    // }
}
</script>

<style>
    .movie {
        min-width: 180px;
        height: 400px;
    }
</style>