<template>
  <div id="app">
<!--     <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <MiComponente></MiComponente>
 -->    
    <HeaderComponent></HeaderComponent>
    <SliderComponent></SliderComponent>
    <div class="center">
      <!-- <LastArticles></LastArticles> -->
      <router-view></router-view>
      <SidebarComponent></SidebarComponent>
    </div>
    <div class="clearfix"></div>
    <FooterComponent></FooterComponent>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue';
//import MiComponente from './components/MiComponente.vue';
import HeaderComponent from './components/HeaderComponent.vue';
import SliderComponent from './components/SliderComponent.vue';
import SidebarComponent from './components/SidebarComponent';
// import LastArticles from './components/LastArticles';
import FooterComponent from './components/FooterComponent';


export default {
  name: 'App',
  components: {
/*     HelloWorld,
    MiComponente,
 */    
    HeaderComponent,
    SliderComponent,
    SidebarComponent,
    // LastArticles,
    FooterComponent
  }
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */

@import './assets/css/style.css';
</style>
