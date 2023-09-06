<template>
    <div>
        <h1 style="text-align: center;">Edit Project {{ id }}</h1>
        <form action=""  @submit.prevent="updateProject">
        <label for="title">Title</label>
        <input type="text" name="" id="title" v-model="title"><br>
        <label for="details">Details</label>
        <input type="text" name="" id="details" v-model="details"><br>
        <button>Update Project</button>
      </form>
    </div>
</template>

<script>
    export default {
        name: 'EditProjectView',
        props: ["id"],
        data() {
            return {
                title: "",
                details: ""
            }
        },
        methods: {
            updateProject() {
                fetch('http://localhost:3000/projects/'+this.id,
                {
                    method: "PATCH",
                    headers: {
                        "Content-Type" : 'application/json'
                    },
                    body: JSON.stringify({
                        title : this.title,
                        details : this.details
                    })
                }
                )
                .then(() => {
                 this.$router.push("/");
                })
                .catch((e) => {
                 console.log(e);
                });
            }
        },
        mounted () {
            fetch('http://localhost:3000/projects/'+this.id).then((response) => {
                 return response.json();
            }).then((data) => {
                this.title = data.title;
                this.details = data.details
            })
            .catch((e) => {
              console.log(e);
            });
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