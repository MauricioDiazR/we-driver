<template>
  <div class="wrapper" :class="{ 'nav-open': $sidebar.showSidebar }">
    <notifications></notifications>

    <side-bar>
      <MobileMenu slot="content"></MobileMenu>

      <sidebar-link to="/app/maps">
        <md-icon>location_on</md-icon>
        <p>Mapa</p>
      </sidebar-link>

      <sidebar-link v-if="user.admin" to="/app/dashboard">
        <md-icon>dashboard</md-icon>
        <p>Dashboard</p>
      </sidebar-link>

      <sidebar-link v-if="user.admin" to="/app/usuarios">
        <md-icon>group</md-icon>
        <p>Usuarios</p>
      </sidebar-link>

      <sidebar-link to="/app/crear">
        <md-icon>input</md-icon>
        <p>Agregar</p>
      </sidebar-link>

      <sidebar-link v-if="user.admin" to="/app/admin">
        <md-icon>settings</md-icon>
        <p>Administración</p>
      </sidebar-link>

      <sidebar-link to="/app/typography">
        <md-icon>library_books</md-icon>
        <p>Cerrar sesión</p>
      </sidebar-link>
    
    </side-bar>

    <div class="main-panel">
      <TopNavbar></TopNavbar>

      <DashboardContent> </DashboardContent>

      <ContentFooter v-if="!$route.meta.hideFooter"></ContentFooter>
    </div>
  </div>
</template>


<style lang="scss"></style>


<script>
import TopNavbar from "./TopNavbar.vue";
import ContentFooter from "./ContentFooter.vue";
import DashboardContent from "./Content.vue";
import MobileMenu from "@/pages/Layout/MobileMenu.vue";

export default {
  data(){
    return{
     
    }
  },
  components: {
    TopNavbar,
    DashboardContent,
    ContentFooter,
    MobileMenu
  },
  computed:{
    user(){
      return this.$store.state.user;
    }
  }
};
</script>
