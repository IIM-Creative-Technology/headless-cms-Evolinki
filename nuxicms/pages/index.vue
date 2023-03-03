<template>
    <div v-if="projects">
        <h1>Bienvenue sur mon portfolio</h1>
        <div v-if="typeprojetenumeration">
            <h5>Selectionne un type de projet</h5>
            <button @click="filterProjects('all')">All</button>
            
            <button v-for="typeProjet in typeprojetenumeration" :key="typeProjet" @click="filterProjects(typeProjet)">
                {{ typeProjet }}
            </button>
            
        </div>
        <h5>Selectionne un projet</h5>
        <nuxt-link :to="`/projects/${project.Slug}`" v-for="project in filteredProjects">{{ project.name }}</nuxt-link>
    </div>
</template>

<script setup>



const { find } = useStrapi()
const projects = ref()
const typeprojetenumeration = ref ([])
const activeFilter = ref ('all')

const filterProjects = (type) => {
        activeFilter.value = type
    }

const filteredProjects = computed(() => {
        if (activeFilter.value === 'all') {
            return projects.value.data
        } else {
            return projects.value.data.filter(project => project.typeprojetenumeration === activeFilter.value)
        }
    })


onMounted(async () => {
    projects.value = await find('projects', { populate: 'deep'})
    typeprojetenumeration.value = new Set(projects.value.data.map(project => project.typeprojetenumeration))


})
</script>

<style>

body {
    background-color: #4d4848;
  }
  
 
  div {
    background-color: #fbfbfb;
    padding: 2rem;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    margin: 2rem auto;
    text-align: center;
    max-width: 600px;
  }
  

  div {
    text-align: center;
  }
  

  img {
    display: block;
    margin: 2rem auto;
    max-width: 100%;
    height: auto;
  }
  
  
  h1:nth-of-type(2) {
    margin-top: 2rem;
    text-align: center;
  }
  

  h1:last-of-type {
    margin-top: 2rem;
    font-size: 1.2rem;
    text-align: center;
  }
  
  
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
  

  nuxt-link {
    display: block;
    margin-top: 1rem;
    text-align: center;
    
  }
  
</style>