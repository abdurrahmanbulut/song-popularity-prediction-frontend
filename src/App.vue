<template>
  <div id="app">
      
    <div class="boddy">
      
      <transition name="toaster">
      <Toaster v-if="showToaster">Feature not available yet</Toaster>
    </transition>
    <router-view ></router-view>
    </div>
    
  </div>
</template>

<script>
  import { mapActions, mapGetters } from 'vuex';
  import router from './router';
  import { setAuthHeader } from './utils/functions';
  import Toaster from './components/Toaster.vue';

  export default {
    name: 'App',
    components: {
      Toaster,
    },
    created() {
      this.$http.interceptors.response.use(
        (response) => {
          return response;
        },
        (error) => {
          if (error.response.status === 401) {
            console.log('Token expired!');
            this.logout();
            router.push({ name: 'login' });
            throw error;
          } else {
            return Promise.reject(error);
          }
        }
      );
    },
    mounted() {
      if (this.$store.getters.isAuthenticated) {
        setAuthHeader(this.$http, this.$store.getters.token);
      } else {
        this.logout();
      }
    },
    computed: {
      ...mapGetters(['displayToaster']),
      showToaster() {
        return this.displayToaster;
      },
    },
    methods: {
      ...mapActions(['logout']),
    },
  };
</script>

<style lang="scss" scoped>

@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Serif&display=swap');


html, body {
font-family: 'IBM Plex Serif', serif;

}

#app{
  width: 100%;
  min-height: 100vh;
  background-color: black;
  display: flex;
  justify-content: center;
  align-items: center;
font-family: 'IBM Plex Serif', serif;

}
.boddy{
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  width:100%;
  background-repeat: no-repeat;
  background-size: cover;
  background-color: #2669a0;
  background-image: linear-gradient(
        -45deg, 
        rgba(59,173,227,1) 0%, 
        rgba(87,111,230,1) 25%, 
        rgba(152,68,183,1) 51%, 
        rgba(255,53,127,1) 100%
  );  
  animation: AnimateBG 20s ease infinite;
}
@keyframes AnimateBG { 
  0%{background-position:0% 50%}
  50%{background-position:100% 50%}
  100%{background-position:0% 50%}
}
</style>
