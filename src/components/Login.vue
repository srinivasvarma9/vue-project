<template>
  <div class="container">
    <form>
      <div class="well">
        <h1>Login Form</h1>
        <h5 v-if="isEditting==true">{{message}}</h5>
        <div class="form-group">
          <label class="pull-left"> Username </label>

          <input
            type="text"
            class="form-control"
            placeholder="Username"
            v-model="User.username"
          />
        </div>

        <div class="form-group">
          <label class="pull-left"> Password </label>

          <input
            type="text"
            class="form-control"
            placeholder="Password"
            v-model="User.password"
          />
        </div>
      </div>

      <button
        class="btn btn-large btn-block btn-success full-width"
       v-on:click.prevent="addToAPI"
      >
        Login
      </button>
      <br>
      Not have a account? Click 
       <router-link to="/Register">

        <button

          type="submit"

          class="btn btn-large  btn-primary full-width"

         >

          Register

        </button>

      </router-link>
    </form>
  </div>
</template>



<script>
/*eslint-disable */

// import axios from "axios";

//import router from '../main';

export default {
  data() {
    return {
    message:'',
    isEditting:false,
      User: {
        username: "",
        password: ""
      }
    }
  },
//   mounted: function(){
//       this.
//   },
  methods: {
    addToAPI() {
      console.log(this.User);
        this.$http.get("http://127.0.0.1:5000/Account/" + this.User.username)
        .then((response) => {
          console.log(response.data[0].username);
             if(this.User.username==response.data[0].username && this.User.password==response.data[0].password){
                this.$router.push({
                    path: "/AccountDetails/"+this.User.username,
                    params:{username:this.User.username}
                }); 
             }

             else{
               
                 this.isEditting=true
                 this.message = "Username/password is wrong"
             }
        //   this.$router.push({
        //     path: "/AccountDetails",
        //   });
        })

        .catch((error) => {
            
            this.isEditting=true
            this.message=error.response.data
          console.log(error.response);
        });
    },
  },
};
</script>

<style scoped>
h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;

  padding: 0;
}

li {
  display: inline-block;

  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>