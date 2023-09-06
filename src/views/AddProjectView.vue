<template>
    <div>
      <form action=""  @submit.prevent="addProject">
        <label for="title">Title</label>
        <input type="text" name="" id="title" v-model="title"><br>
        <label for="details">Details</label>
        <input type="text" name="" id="details" v-model="details"><br>
        <button>Add Project</button>
      </form>
    </div>
</template>

<script>
    export default {
        name: 'AddProjectView',
        data() {
          return {
            title: "",
            details: ""
          }
        },
        methods: {
          addProject() {
            fetch('http://localhost:3000/projects',{
              method : "POST",
              headers: {
                "Content-Type" : "application/json"
              },
              body: JSON.stringify(
                {
                  title: this.title,
                  details: this.details,
                  complete: false
                }
              )
            }).then(() => {
              this.title = "";
              this.details = "";
              this.$router.push({name : 'home'}) //this.$router.push('/')
            });
          }
        },
    }
</script>

<style lang="scss" scoped>
form{
  padding: 10px; 
  border: 1px solid black;
}
label{
  margin-bottom: 10px;
  margin-right: 20px;
}
input{
  margin-bottom: 10px;
}
button{
    float: right;
}
</style>