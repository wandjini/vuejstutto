<template>
<div class="users">
    <h1>Users</h1>
    <form v-on:submit="addUser">
        <input type="text" v-model="newUser.name" placeholder="name">
        <br/>
        <input type="text" v-model="newUser.email" placeholder="email">
        <br/>
        <input type="submit" value="Add User">
    </form>
    <ul>
        <li v-for="user in users" :key="user.email">
            <input type="checkbox" class="toggle" v-model="user.contacted">
            <span :class="{contacted: user.contacted}">
                {{ user.name}} : {{user.email}}<button v-on:click="deleteUser(user)">x</button>
            </span>
            
        </li>
    </ul>
</div>
</template>
<script>
    export default {
        name: 'users',
        data(){
            
            return{
                newUser: {},
                users: [
                    {name: 'John', contacted: true, email: 'john@test.test'},
                    {name: 'Alan', contacted: false, email: 'alan@test.test'} 
                ]
            }
        },
        methods:{
           addUser: function(e){
               e.preventDefault();
               this.users.push({
                   name: this.newUser.name,
                   email: this.newUser.email,
                   contacted: false
               })
           },
           deleteUser: function(user){
               this.users.splice(this.users.indexOf(user),1);
           }
        
        },
        created: function(){
            this.$http.get('https://jsonplaceholder.typicode.com/users')
                .then(function(response){
                    console.log(response.data);
                    this.users = response.data;
                })
            console.log('created Function');
        }
    }
</script>
<style scoped>
    .contacted{
        text-decoration: line-through;
    }
</style>