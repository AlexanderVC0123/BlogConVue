<template>
<div class="general">
  <SliderComponent texto="Bienvenido al Blog con Vue"
   home="true"></SliderComponent>
  <div class="center">
    <section id="content">
      <h2 class="subheader">Ultimos artículos</h2>

      <!--Listado articulos-->
      <div id="articles">
        <article class="article-item" id="article-template">
          <div class="image-wrap">
            <img
              src="https://www.exoticca.com/blog/wp-content/uploads/2019/05/viajes-a-playas-paradis%C3%ADacas-930x360.jpg"
              alt="Playa"
            />
          </div>

          <h2>Articulo de prueba</h2>
          <span class="date"> Hace 5 minutos </span>
          <a href="#">Leer más</a>
          <div class="clearfix"></div>
        </article>
      </div>
    </section>
    <SidebarComponent></SidebarComponent>
    <div class="clearfix"></div>
  </div>
  </div>
</template>

<script>

import SliderComponent from "./SliderComponent.vue";
import SidebarComponent from "./SidebarComponent";

export default {
  name: "LastArticles",
  components: {
    SliderComponent,
    SidebarComponent,
  }
};
</script>
