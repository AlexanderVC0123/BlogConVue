<template>
  <div class="general">
    <div class="center">
      <section id="content">
        <h2 class="subheader">Películas</h2>

        <div class="favorita" v-if="favorita">
            La pelicula favorita es:
            <h3>{{favorita.title}}</h3>
        </div>
        <!--Listado articulos-->
        <div id="articles">
          <div v-for="pelicula in peliculas" v-bind:key="pelicula.title">
            <Pelicula :pelicula="pelicula"
                @favorita="haLlegadoLaPeliculaFav"
            ></Pelicula>
          </div>
        </div>
      </section>
      <SidebarComponent></SidebarComponent>
      <div class="clearfix"></div>
    </div>
  </div>
</template>

<script>
import Pelicula from "./Pelicula.vue";
import SidebarComponent from "./SidebarComponent";

export default {
  name: "Peliculas",
  components: {
    Pelicula,
    SidebarComponent,
  },
  methods: {
      haLlegadoLaPeliculaFav(favorita){
/*           console.log(favorita);
          alert("Se ha ejecutado el evento en el padre");
 */      
    this.favorita = favorita;
    }
  },
  data() {
    return {
        favorita: null,
      peliculas: [
        {
          title: "Batman vs Superman",
          year: 2017,
          image:
            "https://occ-0-1068-92.1.nflxso.net/dnm/api/v6/E8vDc_W8CLv7-yMQu8KMEC7Rrr8/AAAABVixGzDct56-tsHGWLZwtml5CejHjH2jjmxSag8NKtgyx7MNfqzhcC5192uzJoo-dpVg0SvdMiLqD37Sx4-MPCRgK0od.jpg?r=2a9",
        },
        {
          title: "El señor de los anillos",
          year: 2013,
          image:
            "https://arc-anglerfish-arc2-prod-abccolor.s3.amazonaws.com/public/TIPVSN2BUFGFBNPWO4FDSPAH3M.jpg",
        },
        {
          title: "La chaqueta metálica",
          year: 1987,
          image:
            "https://e00-elmundo.uecdn.es/assets/multimedia/imagenes/2018/01/21/15165280933182.jpg",
        },
        {
          title: "Annabelle",
          year: 2018,
          image:
            "https://pics.filmaffinity.com/Annabelle_Creation-137836637-large.jpg",
        },
      ],
    };
  },
};
</script>
