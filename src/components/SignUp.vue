<template>
    <div>
         <h1> Sign Up </h1>
    <div class="register">
        <input type="text" placeholder="Enter First Name" v-model="user_first_name" />
        <input type="text" placeholder="Enter Email" v-model="email" />
        <input type="password" placeholder="Enter Password" v-model="password" />
        <button v-on:click="signup()"> Sign Up </button>
        <div> 
           {questions.map(question=>{
              return ( <h1> {{question.title}}</h1>
               <p>{{question.description}} </p>)
           })}  
         </div>
     </div>
         </div>
   
</template>

<script>
import axios from 'axios'
export default {
    name: 'SignUp',
    data(){
        return {
            user_first_name: "",
            email:"",
            password:"",
            questions:[{
                title:"What is your name?",
                description:"How we will know you"
            }]

        }
    },
    methods: {
        async signup() {
             console.warn('SignUp', this.user_first_name, this.email, this.password);
        let result = await axios.post('http://localhost:4000/users/signup', {
            email:this.email,
            first_name: this.user_first_name,
            password:this.password,
            });
            console.warn(result);
            if(result.status===201){
                alert("SignUp Done")
            }
            localStorage.setItem('user-info',JSON.stringify(result.data))
            this.$router.push({name:'HomePage'})
        }
       
    },
    mounted(){
        let user = localStorage.getItem('user-info');
        if(user){
            this.$router.push({name:'HomePage'})
        }
    }
} 

</script>

<style scoped>
.register input{
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display:block;
    margin:0px auto 30px auto;
    border: 1px solid skyblue;

}

.register button{
    width:320px;
    height: 40px;
    border: 1px solid  goldenrod;
    color:#fff;
    background-color: aquamarine;
    cursor: pointer;
}

</style>


