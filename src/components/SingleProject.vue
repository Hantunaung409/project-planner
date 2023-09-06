<template>
    <div class="single-project">
        <div class="project" :class="{'complete' : projectProp.complete}">
            <div class="titleContainer">
              <h3 @click=" isClicked = !isClicked">{{ projectProp.title }}</h3> 
              <div class="iconsContainer">
                <span @click="deleteProject()"><i class="fa-solid fa-trash"></i></span>   
                <router-link :to="{ name: 'editProject', params: { id :  projectProp.id}}" >
                    <span><i class="fa-solid fa-pen"></i></span>
                </router-link>

                <span @click="completeProject()"><i class="fa-solid fa-check" v-if="!projectProp.complete"></i><i class="fa-solid fa-xmark" v-if="projectProp.complete"></i></span>                
            </div>                  
            </div>
            <p v-if="isClicked">{{ projectProp.details }}</p> 

        </div>
    </div>
</template>

<script>
    export default {
        name: 'SingleProject',
        props: ['projectProp'],
        data() {
            return {
                isClicked: false,
                api: 'http://localhost:3000/projects'
            }
        },
        methods: {
            deleteProject() {
                // console.log(this.projectProp.id);  doesnt need to parse a parameter
                fetch(this.api+'/'+this.projectProp.id,{method: "DELETE"}).then(() => {
                  this.$emit("delete",this.projectProp.id);
                }).catch((e) => { console.log(e);})
            },
            completeProject() {
                fetch(this.api+'/'+this.projectProp.id,{
                    method: "PATCH",
                    headers: {
                        "Content-Type" : "application/json"
                    },
                    body: JSON.stringify(
                        {
                          complete : !this.projectProp.complete
                        }
                    )
                }).then(() => {
                   this.$emit("complete",this.projectProp.id);
                }).catch((e) => {
                   console.log(e);
                });
            }
        },
    }
</script>

<style lang="scss" scoped>
 .project{
    padding: 20px;
    background-color: #f2f2f2;
    margin: 10px;
    border-left: 5px solid crimson;
    border-radius: 8px;
 }
 h3{
    color: indigo;
    cursor: pointer;
 }
 .titleContainer{
    display: flex;
    justify-content: space-between;
    align-items: center;
 }
 .iconsContainer span{
    margin-left: 15px;
    cursor: pointer;
 }
 .iconsContainer span:hover{
    color: #777;
 }
 
 .complete{
    border-left: 5px solid green;
 }
</style>