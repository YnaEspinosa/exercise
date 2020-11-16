<template>
    <div class="container">
        <div class="row">
            <div class="col-3">
                <table class="table table-hover">
                    <thead>
                        <tr>
                            <th scope="col">User</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-bind:key="dataUser.id" v-for="dataUser in dataUsers">
                            <td>
                                <button @click="userPosts(dataUser.id)" type="button" class="btn btn-link">{{dataUser.name}}</button>
                            </td>
                        </tr>
                    </tbody>    
                </table>
            </div>
            <div class="col-9">
                <table class="table">
                    <thead>
                        <th>Post</th>
                    </thead>
                    <tbody>
                      
                            <tr v-bind:key="post.id" v-for="post in posts">
                               <td>
                                    <div class="accordion" id="accordionExample">
                                        <div class="row">
                                            <div class="col-12">
                                                <div class="card">
                                            <div class="card-header" id="headingOne">
                                                <h2 class="mb-0">
                                                    <button class="btn btn-link" type="button" data-toggle="collapse" :data-target="`#collapse${post.id}`" aria-expanded="true" :aria-controls="`collapse${post.id}`">
                                                    {{post.title}}
                                                    </button>
                                                </h2>
                                        </div>

                                        <div :id="`collapse${post.id}`" class="collapse" aria-labelledby="headingOne" data-parent="#accordionExample">
                                        <div class="card-body">
                                            {{post.body}}
                                        </div>
                                        </div>
                                        </div>
                                        </div>
                                    </div>
                                  </div>
                               </td>
                            </tr>
                      
                    </tbody>
                </table>
            </div>
        </div>
    </div>    
</template>

<script>
export default {
    name: "Tables",
    components: {
        
    },
    mounted: function() {
        fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => response.json())
        .then(json => {this.dataUsers = json})
    },

    methods: {
        userPosts(userId) {
            fetch(`https://jsonplaceholder.typicode.com/posts?userId=${userId}`)
            .then(response => response.json())
            .then(json => {this.posts = json})
        }
    },
    data() {
        return {
            dataUsers: [

            ],

            posts: [
            
            ]
        }
    }
    
}
</script>

<style scoped>

</style>