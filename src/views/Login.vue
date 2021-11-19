<template>
  <body>
	<div class="container" id="container">
		<div class="form-container log-in-container">
         <form action="">
           <img class="img-responsive2" src="../assets/logo.png">
            
                <v-form  ref="formLogin" @submit="login">

                          <h1 >LOGIN</h1>
                          
                          <h6>welcome to Mintictiy</h6>

                              <v-text-field class="text2"
                                label="Username"
                                v-model="user"
                                :rules="[validations.required]"
                                @keyup.enter="login"
                              ></v-text-field>
                              <v-text-field class="text2"
                                label="Password"
                                v-model="password"
                                type="password"
                                :rules="[validations.required]"
                                @keyup.enter="login"
                              ></v-text-field>
                              <br>
                  <div class="form-row ">
                     <input type="checkbox" class="checkbox">
                      <span>  Remember</span>
                      <span class="resetpassword">Forget Password? </span>
                 </div>
                  
                </v-form>

                <br>
		    

                 <button class="login-button" @click="login">LOGIN</button>
          </form>
		</div>
		
    <div class="overlay-container">
			<div class="overlay">
			  	<div class="overlay-panel overlay-right ">
               <img class="image" src="../assets/bg.jpg" alt="img">
          </div>
			</div>
		</div>

	</div>
</body>
</template>

<script>
  import jwt from 'jsonwebtoken'

  export default {
    data: () => ({
      user: '',
      password: '',
      validations: {
        required: v => !!v || 'This is a required field!'
      }
    }),
    methods: {
      login() {
        if (this.$refs.formLogin.validate()) {
          jwt.sign({
            user: this.user,
            password: this.password
          }, 'jwtSecret', (err, token) => {
            window.localStorage.setItem('token', token)
            this.$router.push('/')
          })
        }
      }
    }
  }
</script>

<style scoped>

* {
	box-sizing: border-box;
}

body {
	background:  #2B4255;
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
	font-family: 'Montserrat', sans-serif;
	height: 100vh;

}
.form-row {
min-width: 100%;
align-content: space-between;
}

h1 {
  padding-top: 80px;
	font-weight: bold;
	margin: 0;
  text-align: center;
}

h6 {
	font-size: 12px;
  margin: 0;
  text-align: center;
  padding-top: 10px;
  padding-bottom: 40px;
}

.resetpassword{
float: right;

}

.checkbox{
float: left;
margin-right: 3px;

}

button {
  background-color: #2B4255;
  color: #ffffff;
  font-size: 1.3em;
  font-weight: 600;
  border-radius: 50px;
  height: 55px;
  width: 160px;
  align-content: center;
  
}

form {
	background-color: #FFFFFF;
	display: flex;
	align-items: center;
	justify-content: center;
	flex-direction: column;
	padding: 0 10px;
}

.text2 {
	margin: 0;
  text-align: center;
  margin-top: 10px;
  margin-bottom: 10px;
  width: 250px;
  background-color: #E3E7F1;
  border-radius: 30px;
  max-height: 50px;
  border-style: none;

  }

.container {
	background-color: #fff;
	border-radius: 35px;
  box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
	position: relative;
	overflow: hidden;
	width: 700px;
	max-width: 100%;
  max-height: 70%;
	min-height: 600px;
}

.form-container {
	position: absolute;
	top: 0;
	height: 100%;
}

.log-in-container {
	left: 0;
	width: 50%;
	z-index: 2;
}

.overlay-container {
	position: absolute;
	top: 0;
	left: 50%;
	width: 50%;
	height: 100%;
}

.overlay {
	background-repeat: no-repeat;
	background-size: cover;
	background-position: 0 0;
	color: #FFFFFF;
	position: relative;
	left: -100%;
	height: 100%;
	width: 200%;
}

.overlay-panel {
	position: absolute;
	display: flex;
	align-items: center;
	justify-content: center;
	flex-direction: column;
	text-align: center;
	top: 0;
	height: 100%;
	width: 50%;
}

.overlay-right {
	right: 0;
   
}
.image{
    position: absolute;
    height: 100%;
    left: 0;
    
}


</style>


