<template>
  <div class=" max-w-6xl h-1000px m-auto p-10">
    <h2 class="text-2xl font-bold mb-8">{{titulo}}</h2>
    
      
      <div class="container-movie">
        <Movie v-for="(movie, index) in movies" :key="index" :img_url="movie.img_path" :title="movie.title" :release_date="movie.release_date_string" :days_to_release="movie.days_to_release"/>
        
      </div>
      
      
    
  </div>
</template>

<script>
import Movie from './Movie.vue'
import moment from 'moment'
import axios from 'axios'



export default {
  



    name: 'MovieSection',
    props: {
      titulo: {
        type: String,
        required: true,
      },
    },
    data() {
      return {
        page: 1,
        date: '',
        movies: []
      }
    },
    components: {
      Movie,
    },
    methods: {
      getMovies(){
        
        axios.interceptors.response.use(res => {
            const base_url_img ='http://image.tmdb.org/t/p/'
            const size = 'w154/'
            const movies = res.data.results.map(e => {
              
              e.full_img_path = `${base_url_img}${size}${e.poster_path}`

              const release_date = this.formatDate(e)

              const days_to_release = this.daysToRelease(e.release_date)
              return {
                title: e.title,
                img_path: e.full_img_path,
                release_date_string: release_date,
                days_to_release: days_to_release.toFixed(0),
              }

            })

          return movies
        })

        const url = `https://api.themoviedb.org/3/discover/movie?api_key=fc39de80b27fbee5fdd0cb397974ab16&language=pt-BR&sort_by=popularity.desc&include_adult=false&include_video=false&page=${this.page}&primary_release_date.gte=${this.date}&with_watch_monetization_types=flatrate`

        axios.get(url).then(res => {
          if(res){
              this.movies.push(...res)
              this.page++
              console.log(`click ${this.page}`)
              console.log(this.movies)
              console.log(res)
          } 
        })

    },
    searchMovies(movie){
      if(movie){
        const url = `https://api.themoviedb.org/3/search/movie?api_key=fc39de80b27fbee5fdd0cb397974ab16&language=pt-BR&query=${movie}&page=1&include_adult=false`

        axios.get(url)
        .then(res => {
          this.movies = res
         })
      } else {
        this.getMovies()
      }
      
    },
    

    daysToRelease(release_date){
        const dateRelease = moment(release_date)
        const today = moment()
        const diff = moment(dateRelease, "DD/MM/YYYY HH:mm:ss").diff(moment(today, 'DD/MM/YYYY HH:mm:ss'))
        const days = moment.duration(diff).asDays()
      
        return days
      },

    formatDate(movie) {

        let new_date = moment(movie.release_date).format('DD/MM/YYYY')
        return new_date
        
      }
    
    },
    mounted(){
      

      this.emitter.on('search', this.searchMovies)
      this.date = moment().format('YYYY-MM-DD')
      this.getMovies()
      
    }
    
}
</script>

<style scoped>

  /* Works on Chrome, Edge, and Safari */
  *::-webkit-scrollbar {
    width: 5px;
    height: 8px;
  }
  
  *::-webkit-scrollbar-track {
    background: transparent;
    border-radius: 5px;
  }
  
  *::-webkit-scrollbar-thumb {
    background-color:  rgba(71, 3, 3, 0.459)   ;
    border-radius: 20px;
    border: 1px solid rgba(71, 3, 3, 0.459);
  }

    .container-movie {
      display: flex;
      flex-wrap: nowrap;
      overflow-x: auto;
    }

    
</style>