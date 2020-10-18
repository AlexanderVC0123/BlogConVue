<template>
  <div class="general">
    <SliderComponent texto="Blog"></SliderComponent>
    <div class="center">
      <section id="content">
        <h2 class="subheader">Blog</h2>
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
  name: "Blog",
  components: {
    SliderComponent,
    SidebarComponent,
  },
};
</script>