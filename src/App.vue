<template>
  <!-- RECEBER VARIAVEIS SEMPRE TEM QUE SER BINDADA -->
<Navbar :logo="logoApp" :alt="altApp" />
<!-- A VIEW É IMPRESSA NESSE ROUTER-VIEW -->
<router-view/>
<Footer />
</template>

<script>

import Navbar from '../src/components/Navbar.vue'
import Footer from '../src/components/Footer.vue'
export default ({

  data() {
    return{
      logoApp: './img/pngwing.com.png',
      altApp: 'Açai Store'
    }
  },

  components: {
    Navbar,
    Footer
  }
 
})
</script>

<style>
* {
  font-family: Arial, Helvetica, sans-serif;
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}

.main-container{
  margin: 50px;
  min-height: 250px;

}
.main-container h1 {
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}


</style>
