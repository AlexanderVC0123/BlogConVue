<template>
  <div class="general">
    <div class="center">
      <section id="content">
        <article
          class="article-item article-detail"
          id="article-template"
          v-if="article"
        >
          <div class="image-wrap">
            <img
              :src="url + 'get-image/' + article.image"
              :alt="article.title"
              v-if="article.image"
            />
            <img
              src="../assets/images/default.png"
              :alt="article.title"
              v-else
            />
          </div>

          <h1 class="subheader">{{ article.title }}</h1>
          <span class="date"> {{ article.date | moment("from", "now") }} </span>
          <p>
            {{ article.content }}
          </p>
          <div class="clearfix"></div>
        </article>
      </section>
      <SidebarComponent></SidebarComponent>
      <div class="clearfix"></div>
    </div>
  </div>
</template>

<script>
import SidebarComponent from "./SidebarComponent";
import { Global } from "../Global";
import axios from "axios";

export default {
  name: "Article",
  components: {
    SidebarComponent,
  },
  data() {
    return {
      url: Global.url,
      article: null,
    };
  },
  mounted() {
    var articleId = this.$route.params.id;
    this.getArticle(articleId);
  },
  methods: {
    getArticle(articleId) {
      axios.get(this.url + "article/" + articleId).then((res) => {
        if (res.data.status === "success") {
          this.article = res.data.article;
        }
      });
    },
  },
};
</script>