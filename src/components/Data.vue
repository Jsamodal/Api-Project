<template>
    <div class="container">
        <input type="text" v-model="search" placeholder="Search by Name"/> 
        <ul class="info" v-for="user in filteredUsers" :key="user.firstName">
                 <img v-bind:src="user.pic" class='profilepicture'/>
                 <div class="info-container">
                <h1>{{user.firstName.toUpperCase()}} {{user.lastName.toUpperCase()}} </h1>
                <p>Company: {{user.company}}</p>
                <p>Email: {{user.email}}</p>
                <p>Skill: {{user.skill}}</p>
                <p>Average: {{onAverage(user.grades)}}%</p>
                <button v-on:click="!hidden">+</button> 
                <ul><li v-for="(grade, index) in user.grades" :key="index" v-show="hidden === false" > Test {{index}}:{{grade}}</li>  </ul>
                    
                
                </div>
            
        </ul>
    </div>
</template>

<script>
const axios = require('axios').default;


export default {
    
    name: 'Data',
    data() {
            return {
                users: [],
                search: "",
                hidden : true,
                grades : []
            }
        },

    mounted: function() {
        
        axios.get('https://api.hatchways.io/assessment/students')
        .then(response =>  {
            this.users = response.data.students
            console.log(this.users);
             })
        .catch(error => {
            console.log(error);
        });

    },
    methods: {


        onAverage(arr){
            let NumArray = arr.map(element => parseInt(element))

            let sum = NumArray.reduce((total, currentValue) => total+currentValue )

            let avg = sum / NumArray.length 

            return avg
        }
    },

    computed: {
        filteredUsers() {
            return  this.users.filter(post => post.firstName.toLowerCase().match(this.search)|| post.lastName.toLowerCase().match(this.search))
        }

            
        
    }
}
</script>

<style scoped>

.container {
  box-sizing: border-box;
  max-width: 65%;
  margin: 30px auto;
  overflow: auto;
  height:500px;
  max-height: 80%;
  border: 1px solid white;
  padding: 40px;
  
}
.profilepicture{
    position: relative;
    right:40px;
    height:10%;
    width:100px;
    border-radius:50%;
    border:1px solid rgb(228, 224, 224);
    z-index:2;
}
.info-container{
    position: relative;
    bottom:100px;
    z-index:1;
}
.info{
    display:flex;
    flex-direction: column;
    border-bottom: .1px solid rgb(228, 224, 224);
}

*{
    background-color: white;
}

</style>