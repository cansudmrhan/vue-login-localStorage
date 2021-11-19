<template>
  <body>   
    <div class="bg">
          <nav class="navbar navbar-expand-sm ">
          <div class="container-fluid">	  
            <div class="navbar-nav .me-auto">
                  <img class="img-responsive2" src="../assets/logo.png">
            </div>
            <v-btn class="navbar-nav .ms-auto" @click="logout"> <i class="fa fa-close"></i> </v-btn>
          </div> 
          </nav>
          
          <div class="welcome">
            <v-model name="text" id="text" > <strong>WELCOME : {{ loggedUser.user }} !</strong> </v-model>
          </div>
    </div>
  </body>
</template>

<script>
  export default {
    data: () => ({
      logged: false,
    }),
    methods: {
      isLogged() {
        window.localStorage.getItem('token')
          ? this.logged = true
          : this.logged = false
      },
      logout() {
        window.localStorage.removeItem('token')
        this.$router.push('/login')
      }
    },
    computed: {
      loggedUser() {
        const token = window.localStorage.getItem('token')
        const payload = JSON.parse(atob(token.split('.')[1]))
        return payload
      }
    },
    mounted() {
      this.isLogged()
    }
  }
</script>


<style scoped>

body, html {
  height: 100%;
  margin: 0;
  font: 400 15px/1.8 "Lato", sans-serif;
  
} 

.bg {
  background : url('../assets/bg.jpg') no-repeat center center fixed;
  position: relative;
  opacity: 0.65;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  height: 100%;
 
}

.navbar{ 
     overflow: hidden;
     margin-top : -5px ;
     opacity: 1.5;
     background-image: linear-gradient(to right, #FFFFFF 85%, #E3E7F1 100%)

}

.welcome{
  position: absolute;
  left: 0;
  top: 50%;
  width: 100%;
  font-size: 32px;
  text-align: center;
  color: #2B4255;
  opacity: 1.5;
}

 .logo-image{
    width: 46px;
    height: 46px;
    border-radius: 50%;
    overflow: hidden;
    margin-top: -6px;
}


</style>
