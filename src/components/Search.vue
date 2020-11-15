<template>
  <div class="general">
    <SliderComponent :texto="'Busqueda: '+ searchString"></SliderComponent>
    <div class="center">
      <section id="content">

        <h1 class="subheader" v-if="articles">Articulos encontrados</h1>
        <h1 class="subheader" v-else>Sin resultados</h1>

        <div id="articles" v-if="articles">
          <Articles :articles="articles"></Articles>
        </div>
        <div v-else>
            <h2> No hay artículos que coincidan con tu búsqueda</h2>
        </div>

      </section>
      <SidebarComponent></SidebarComponent>
      <div class="clearfix"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { Global } from "../Global"

import SliderComponent from "./SliderComponent.vue";
import SidebarComponent from "./SidebarComponent";
import Articles from './Articles';

export default {
  name: "Search",
  components: {
    SliderComponent,
    SidebarComponent,
    Articles

  },
  mounted() {
    this.searchString = this.$route.params.searchString;
    this.getArticlesBySearch(this.searchString);
  },
  data() {
    return {
      articles: [],
      url: Global.url,
      searchString: null
    };
  },
  methods: {
    getArticlesBySearch(searchString) {
      axios.get(this.url+"search/"+searchString).then((res) => {
        if (res.data.status === "success") {
          this.articles = res.data.articles;
          console.log(this.articles);
        }
      });
    },
  },
};
</script>