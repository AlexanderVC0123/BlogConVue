<template>
  <div class="general">
    <SliderComponent texto="Blog"></SliderComponent>
    <div class="center">
      <section id="content">
        <h2 class="subheader">Blog</h2>

        <div id="articles" v-if="articles">
          <Articles :articles="articles"></Articles>
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
  name: "Blog",
  components: {
    SliderComponent,
    SidebarComponent,
    Articles

  },
  mounted() {
    this.getArticles();
  },
  data() {
    return {
      articles: [],
      url: Global.url
    };
  },
  methods: {
    getArticles() {
      axios.get(this.url+"articles").then((res) => {
        if (res.data.status === "success") {
          this.articles = res.data.articles;
          console.log(this.articles);
        }
      });
    },
  },
};
</script>