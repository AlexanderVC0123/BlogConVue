<template>
  <div class="general">
    <div class="center">
      <section id="content">
        <h1 class="subheader" v-if="!isEdit">Crear artículo</h1>
        <h1 class="subheader" v-else>Editar artículo</h1>

        <!--Formulario-->
        <form class="mid-form" @submit.prevent="save()">
          <div class="form-group">
            <label for="title">Título</label>
            <input type="text" name="title" v-model="article.title" />
            <div v-if="submitted && !$v.article.title.required">
              Pon un titulo a tu artículo!
            </div>
          </div>

          <div class="form-group">
            <label for="content">Contenido</label>
            <textarea name="content" v-model="article.content"></textarea>
            <div v-if="submitted && !$v.article.content.required">
              Necesitas rellenar este apartado!
            </div>
          </div>

          <div class="form-group">
            <div v-if="isEdit && article.image">
              <img
                :src="url + 'get-image/' + article.image"
                :alt="article.title"
                v-if="article.image"
                class="image-small"
              />
            </div>
            <label for="image">Imagen</label>
            <input
              type="file"
              id="file"
              ref="file"
              name="file0"
              v-on:change="fileChange()"
            />
          </div>
          <div class="clearfix"></div>

          <input type="submit" value="Guardar" class="btn btn-success" />
        </form>
      </section>
      <SidebarComponent></SidebarComponent>
      <div class="clearfix"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { Global } from "../Global";
import { required } from "vuelidate/lib/validators";
import swal from "sweetalert";

import SidebarComponent from "./SidebarComponent";
import Article from "../models/Article";

export default {
  name: "EditArticle",
  components: {
    SidebarComponent,
  },
  data() {
    return {
      url: Global.url,
      file: "",
      article: new Article("", "", null, ""),
      submitted: false,
      isEdit: true,
    };
  },
  validations: {
    article: {
      title: {
        required,
      },
      content: {
        required,
      },
    },
  },
  mounted() {
    //console.log(this.article);
    var articleId = this.$route.params.id;
    this.getArticle(articleId);
  },
  methods: {
    
    getArticle(articleId) {
      axios.get(this.url + "article/" + articleId).then((res) => {
        if (res.data.status == "success") {
          this.article = res.data.article;
        }
      });
    },fileChange() {
      this.file = this.$refs.file.files[0];
      console.log(this.file);
    },
    save() {
      this.submitted = true;
      var articleId = this.$route.params.id;

      this.$v.$touch();
      if (this.$v.$invalid) {
        return false;
      } else {
        axios
          .put(this.url + "article/" + articleId, this.article)
          .then((res) => {
            if (res.data.status == "success") {
              //Subida de archivo
              if (
                this.file != null &&
                this.file != undefined &&
                this.file != ""
              ) {
                const formData = new FormData();
                formData.append("file0", this.file, this.file.name);
                //Obtener el id
                this.article = res.data.article;
                var articleId = res.data.article._id;
                //Guardar foto
                axios
                  .post(this.url + 'upload-image/' + articleId, formData)
                  .then(res => {
                    if (res.data.article) {
                      swal(
                        "Articulo editado",
                        "El articulo se ha editado correctamente con foto",
                        "success"
                      );

                      this.article = res.data.article;
                      this.$router.push("/articulo/"+this.article._id);
                    } else {
                      //Mostrar alerta de error
                      swal(
                        "Articulo no se editado",
                        "El articulo no se ha editado correctamente",
                        "error"
                      );
                    }
                  })
                  .catch((err) => {
                    console.log(err);
                  });
              } else {
                swal(
                  "Articulo editado",
                  "El articulo se ha editado correctamente sin foto",
                  "success"
                );

                this.article = res.data.article;
                this.$router.push("/articulo/" + this.article._id);
              }
            }
          })
          .catch((err) => {
            console.log(err);
          });
      }
    },
  },
};
</script>