<template>
  <div class="general">
    <div class="center">
      <section id="content">
        <h1 class="subheader">Crear artículo</h1>

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
import swal from 'sweetalert';

import SidebarComponent from "./SidebarComponent";
import Article from "../models/Article";

export default {
  name: "CreateArticle",
  components: {
    SidebarComponent,
  },
  data() {
    return {
      url: Global.url,
      file: "",
      article: new Article("", "", null, ""),
      submitted: false,
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
    console.log(this.article);
  },
  methods: {
    fileChange() {
      this.file = this.$refs.file.files[0];
      console.log(this.file);
    },
    save() {
      this.submitted = true;

      this.$v.$touch();
      if (this.$v.$invalid) {
        return false;
      } else {
        axios
          .post(this.url + "save", this.article)
          .then((res) => {
            if (res.data.status === "success") {
              //Subida de archivo
              if (
                this.file != null &&
                this.file != undefined &&
                this.file != ""
              ) {
                const formData = new FormData();
                formData.append("file0", this.file, this.file.name);

                var articleId = res.data.article._id;
                axios
                  .post(this.url + "upload-image/" + articleId, formData)
                  .then((res) => {
                    if (res.data.article) {

                      swal(
                        'Articulo creado',
                        'El articulo se ha creado correctamente',
                        'success'
                      );

                      this.article = res.data.article;
                      this.$router.push("/blog");
                    } else {
                      //Mostrar alerta de error
                      swal(
                        'Articulo no se creado',
                        'El articulo no se ha creado correctamente',
                        'error'
                      );
                    }
                  })
                  .catch((err) => {
                    console.log(err);
                  });
              } else {

                swal(
                        'Articulo creado',
                        'El articulo se ha creado correctamente',
                        'success'
                      );

                this.article = res.data.article;
                this.$router.push("/blog");
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