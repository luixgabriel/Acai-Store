<template>
    <div id="main-banner">
        <h1>AÇAI STORE</h1>
    </div>
  
</template>

<script>
export default {
    name: 'Banner'
}
</script>

<style scoped>
#main-banner{
    /* BUSCAR DIRETO NA PASTA PUBLIC */
    background-image: url('/public/img/acaiBG.png');
    background-position: 0 -130px;
    background-size: cover;
    background-repeat:no-repeat ;
    height: 500px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
   
}
#main-banner h1{
    color: rgb(224, 69, 69);
    border-radius: 40px;
    margin-left: 8px;
    text-align: center;
    background-color: #222;
    padding: 20px 40px;
}

@media screen and (max-width: 600px) {
    #main-banner {
    background-image: none;
    height: 500px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgb(224, 69, 69);

  
    }


}
</style>