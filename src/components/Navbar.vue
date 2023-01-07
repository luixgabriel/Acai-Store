<template>
  <nav id="nav">
    <router-link to="/" id="logo-url">
        <img :src="logo" :alt="alt" id="logo">
    </router-link>
    <router-link to="/">Home</router-link> 
    <router-link to="/Pedidos">Pedidos</router-link>
  </nav>
</template>

<script>
export default {
name: 'Navbar',
data(){
  return {

  }
},
props: ['logo', 'alt']

}
</script>

<style scoped>

#nav{
  background-color: #222;
  border-bottom: 4px solid rgb(224, 69, 69);
  padding: 8px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;


}
#logo {
  width: 60px;
  height: 60px;
  
}
#nav #logo-url {
  margin: auto;
  margin-left: 0px;
}
#nav a {
  color: rgb(224, 69, 69);
  text-decoration: none;
  transition: .5s;
  margin: 12px;
  font-size: 1.5rem;
}

#nav a:hover{
  color: #fff;
}
</style>