<template>
<div class="test">
    <h1>{{title}}</h1>
    <h2>{{msg}}</h2>
    <input type="text" v-model="title"><br/>
    <p>{{user.firstName}}</p>
    <p v-text="user.firstName"></p>
    <p v-if="showName">{{user.lastName}}</p>
    <p v-else>No Body</p>
    <ul>
        <li v-for="item in items" :key="item.title">
            {{item.title}}
        </li>
    </ul>
    <button v-on:click="greet('Ciao Mondo')">Say Greeting</button>
    <input type="text" v-on:keyup="pressKey" v-on:keyup.enter="enterHit">
    <hr />
    <label>First name</label>
    <input type="text" v-model="user.firstName" ><br/>
    <label>Last name</label>
    <input type="text" v-model= "user.lastName" >
    <h3>
        {{fullName}}
    </h3>
    

</div>
</template>
<script>
    export default {
        name: 'test',
        props: {
            msg: {
                default: 'Foobar',
                type: String
            }
        },
        data(){
            return{
                title: 'Hello World',
                user:{
                    firstName: 'John',
                    lastName: 'Doe'
                },
                showName: false,
                items: [
                    {title: 'Item One'},
                    {title: 'Item Two'} 
                ]
            }
        },
        methods:{
           greet: function(greeting){
               alert(greeting);
           },
           pressKey: function(e){
               console.log(e.target.value);
           },
           enterHit: function(){
               console.log('You Hit Enter')
           }
        
        },
           computed: {
               fullName: function(){
                   return this.user.firstName + ' ' + this.user.lastName;
               }
           } 
        
    }
</script>
<style scoped>
</style>