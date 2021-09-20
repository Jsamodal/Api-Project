<template>
    <div class="container">
        <ul class="info" v-for="user in users.students">
                 <img v-bind:src="user.pic" class='profilepicture'/>
                 <div class="info-container">
                <h1>{{user.firstName.toUpperCase()}} {{user.lastName.toUpperCase()}} </h1>
                <p>Company: {{user.company}}</p>
                <p>Email: {{user.email}}</p>
                <p>Skill: {{user.skill}}</p>
                <!-- <p v-for="grade in user.grades">{{onAverage(grade)}}</p> -->
                <p>Average: {{onAverage(user.grades)}}%</p>
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
                users: []
            }
        },

    mounted: function() {
        axios.get('https://api.hatchways.io/assessment/students')
        .then(response =>  {
            this.users = response.data
            console.log(response.data);
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