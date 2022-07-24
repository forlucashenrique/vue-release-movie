<template>
      <Header />
        
      <MovieSection titulo="Próximos Lançamentos"/>
        
      <Footer />
</template>

<script>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import MovieSection from './components/MovieSection.vue'



export default {
  name: 'App',
  components: {
    Header,
    Footer,
    MovieSection
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  /* box-sizing: border-box; */
}

body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  width: 100%;
}


</style>
