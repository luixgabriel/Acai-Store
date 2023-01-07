<template>
  <Banner />
  <div class="main-container">
    <h1>Monte seu Açai:</h1>
    <FormPed />
  </div>
  
</template>


<script>

import Banner from '../components/Banner.vue'
import FormPed from '../components/FormPed.vue'
export default {
  name: 'HomeView',
  components: {
    Banner, FormPed
  }
}
</script>
