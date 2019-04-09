<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 Top Vuesic Mexico
    select(v-model="paisSelecto")
        option(v-for="(pais, index) in paises" :key="index" :value="pais.value") 
            span {{pais.name}}
    loader(v-if="loading")
    ul(v-else)
        artista(v-for="(artista, index) in artistas" :artista="artista"  :key="artista.mbid")


</template>

<script>
import Artista from "./components/artista.vue";
import Loader from "./components/loader.vue";
import getArtists from "./api";
export default {
    name: "app",
    data() {
        return {
            artistas: [],
            paises: [
                { name: "Mexico", value: "mexico" },
                { name: "España", value: "spain" },
                { name: "Suecia", value: "sweden" }
            ],
            paisSelecto: "mexico",
            loading: true
        };
    },
    methods: {
        actualizarArtistas() {
            const self = this;
            self.loading = true;
            self.artistas = [];
            getArtists(self.paisSelecto).then(val => {
                self.loading = false;
                self.artistas = val;
            });
        }
    },
    mounted() {
        const self = this;
        getArtists(self.paisSelecto).then(val => {
            self.loading = false;
            self.artistas = val;
        });
    },
    watch: {
        paisSelecto() {
            this.actualizarArtistas();
        }
    },
    components: {
        Artista,
        Loader
    }
};
</script>

<style lang="scss" scoped>
#app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

h1,
h2 {
    font-weight: normal;
}

ul {
    list-style-type: none;
    padding: 0;
}

li:artista {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}
</style>
