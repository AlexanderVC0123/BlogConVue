<template>
  <div class="general">
    <div class="center">
      <section id="content">
        <h1 class="subheader">Crear artículo</h1>

        <!--Formulario-->
        <form class="mid-form" @submit.prevent="save()">
            <div class="form-group">
                <label for="title">Título</label>
                <input type="text" name='title' v-model="article.title"/>
            </div>

            <div class="form-group">
                <label for="content">Contenido</label>
                <textarea name='content' v-model="article.content"></textarea>
            </div>

            <div class="form-group">
                <label for="image">Imagen</label>
                <input type="file" name='image' />
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

/* import axios from "axios";
import { Global } from "../Global"
import { required, minLength} from 'vuelidate/lib/validators'
 */
import SidebarComponent from "./SidebarComponent";
import Article from '../models/Article'

export default {
    name: 'CreateArticle',
    components: {
        SidebarComponent,
    }, 
    data(){
        return{
            article: new Article('', '', null, '')
        }
    },
    mounted(){
        console.log(this.article)
    },
    methods: {
        save(){
            console.log(this.article)
        }
    }
}
</script>