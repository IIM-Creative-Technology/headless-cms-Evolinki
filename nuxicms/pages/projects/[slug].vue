<template>
    
    <div v-if="project">
        <img :src="project.picture.url" alt="" width="500">
        <h1> {{ project.name }}</h1>
        <h3 v-for="technologie in project.technologies">Techno:{{ technologie.nomtechno }}</h3>
        <h1>"{{ project.description }}"</h1>
        <a href="http://localhost:3000">Précédent</a>
        <nuxt-link :to="project.url" target="_blank">Lien du projet</nuxt-link>
        
    </div>
   
</template>

<script setup>



const {findOne} = useStrapi()
const route = useRoute()
const project = ref()

onMounted(async() => {
    project.value = await findOne(`projects?filters[slug]=${route.params.slug}&populate=*`)
    project.value = project.value.data[0]
    console.log(project)

})



</script>
<style>
/* couleur d'arrière-plan de la page */
body {
    background-color: #4d4848;
  }
  
  /* couleur d'arrière-plan du conteneur principal */
  div {
    background-color: #fbfbfb;
    padding: 2rem;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    margin: 2rem auto;
    text-align: center;
    max-width: 600px;
  }
  
  /* centrage horizontal pour les éléments de niveau de bloc */
  div {
    text-align: center;
  }
  
  /* centrage vertical et horizontal pour l'image du projet */
  img {
    display: block;
    margin: 2rem auto;
    max-width: 100%;
    height: auto;
  }
  
  /* centrage vertical pour les titres des technologies */
  h1:nth-of-type(2) {
    margin-top: 2rem;
    text-align: center;
  }
  
  /* centrage vertical pour la description du projet */
  h1:last-of-type {
    margin-top: 2rem;
    font-size: 1.2rem;
    text-align: center;
  }
  
  /* centrage vertical pour les liens */
  a {
    display: inline-block;
    margin-top: 1rem;
    padding: 0.5rem 1rem;
    background-color: #101112;
    color: #fff;
    text-decoration: none;
    border-radius: 5px;
    transition: background-color 0.3s ease;
    text-align: center;
  }
  
  /* centrage vertical pour le lien du projet */
  nuxt-link {
    display: block;
    margin-top: 1rem;
    text-align: center;
    
  }
  
</style>
