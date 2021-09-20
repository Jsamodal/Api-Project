<template>
    <div class="container">
        <ul v-for="user in users.students">
            <ul>
                 <img v-bind:src="user.pic" />
                <h1>{{user.firstName}} {{user.lastName}} </h1>
                <p>Company: {{user.company}}</p>
                <p>Email: {{user.email}}</p>
                <p>Skill: {{user.skill}}</p>
                <!-- <p v-for="grade in user.grades">{{onAverage(grade)}}</p> -->
                <p>Average: {{onAverage(user.grades)}}%</p>
            </ul>
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
            let output = []

            for ( let num of arr){
            let suum = parseInt(num)
            output.push(suum)
        
            const reducer = (previousValue, currentValue) => previousValue + currentValue;
            const sum = output.reduce(reducer)
            const avg = sum / arr.length
            return avg

            // for (let value of arr) {
            //     let array = []
            //     let values = parseInt(value)
            //     let newArray = array.push(values)
            //     console.log(values)

            }
        
        //     const reducer = (previousValue, currentValue) => previousValue + currentValue;
        //     const sum = arr.reduce(reducer)
        //     console.log(sum)
        }
    }
}
</script>

<style scoped>
    * {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
    font-family: 'Raleway', sans-serif;;
}
.container {
    box-sizing: border-box;
  max-width: 80%;
  margin: 30px auto;
  overflow: auto;
  height:500px;
  max-height: 80%;
  border: 1px solid steelblue;
  padding: 40px;
  border-radius: 5px;
}

</style>