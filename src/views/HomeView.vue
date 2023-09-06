<template>
  <div class="home">
   <FilterNav @filterValue="currentFilterValue = $event"></FilterNav>
   <div class="" v-for="project in filterProjects" :key="project.id">
     <SingleProject :projectProp="project" @delete="deleteProject" @complete="completeProject"></SingleProject> <!--You cannot add () at deleteProject-->
   </div>
  </div>
</template>

<script>
import FilterNav from '../components/FilterNav'
import SingleProject from '../components/SingleProject'
// @ is an alias to /src
export default {
  components: {
    FilterNav, SingleProject },
  name: 'HomeView',
  data() {
    return {
      projects: [],
      currentFilterValue: "all"
    }
  },
  methods: {
    deleteProject(deletedId) {
      this.projects = this.projects.filter( project => {
        return project.id != deletedId ;
      })
    },
    completeProject(completedId){
      let completedProject = this.projects.find(project=>{
        return project.id === completedId;
      });
      completedProject.complete = !completedProject.complete;  //if change the value of find ... the original array is affected & if u log only the single data is outputed
    }
  },
  computed: {
    filterProjects() {
      if(this.currentFilterValue === "onGoing"){
        return this.projects.filter((project) => {
          return project.complete == false;
        })
      }
      if(this.currentFilterValue === "Complete"){
        return this.projects.filter((project) => {
          return project.complete == true;
        })
      }
      return this.projects 
    }
  },
  mounted () {
    fetch('http://localhost:3000/projects').then((response) => {
      return response.json() //cant read the response so turn into json and return to first then
    }).then((data) => {
       //cath the json data from the first then with the second then
      this.projects = data;
    })
    .catch((e) => {
      console.log(e);
    });
  },
}
</script>
