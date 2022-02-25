<template>
  <div>
  <nav-bar />
  <div class="card">
  <div class="container">
    <div class="f-b">
    <form @submit.prevent="registerUser">
      <div class="row">
      <v-icon class="mr-2">mdi-account</v-icon>
      <v-text-field
        v-model="name"
        :error-messages="nameErrors"
        :counter="10"
        label="Name"
        required
        @input="$v.name.$touch()"
        @blur="$v.name.$touch()"
      ></v-text-field>
      </div>
      <div class="row">
        <v-icon class="mr-2">mdi-email</v-icon>
      <v-text-field
        v-model="email"
        :error-messages="emailErrors"
        label="E-mail"
        required
        @input="$v.email.$touch()"
        @blur="$v.email.$touch()"
      ></v-text-field>
      </div>
      <div class="row">
        <v-icon class="mr-2">mdi-key</v-icon>
      <v-text-field
        v-model="password"
        :error-messages="passwordErrors"
        label="Password"
        required
        @input="$v.password.$touch()"
        @blur="$v.password.$touch()"
      ></v-text-field>
      </div>
    
      <v-btn
        block
        class="mr-4 mt-8 indigo lighten-3"
        type="submit"
      >
        submit
      </v-btn>
    </form>
    </div>
    <div class="cover back">
        <img class="backImg" src="https://i.pinimg.com/originals/45/5b/0c/455b0c8f69ca0c63f09301e71f98880e.jpg" alt="background" />
        <div class="text">
          <span class="text-1">Complete miles of journey <br> with one step</span>
          <span class="text-2">Let's get started</span>
        </div>
      </div>
  </div>
  </div>
  <Footer />
  </div>
</template>

<script>
import axios from 'axios'
import NavBar from '../components/NavBar.vue'
import Footer from '../components/Footer.vue'
import { validationMixin } from 'vuelidate'
import { required, maxLength, email, minLength } from 'vuelidate/lib/validators'

export default {
  name: 'SignUp',
  mixins: [validationMixin],
  components: {
    NavBar,
    Footer
  },
    validations: {
        name: { required, maxLength: maxLength(10) },
        email: { required, email },
        password: {required, minLength: minLength(8) },
    },

    data: () => ({
        name: '',
        email: '',
        password: ''
    }),

    computed: {
        nameErrors () {
        const errors = []
        if (!this.$v.name.$dirty) return errors
        !this.$v.name.maxLength && errors.push('Name must be at most 10 characters long')
        !this.$v.name.required && errors.push('Name is required.')
        return errors
        },
        emailErrors () {
        const errors = []
        if (!this.$v.email.$dirty) return errors
        !this.$v.email.email && errors.push('Must be valid e-mail')
        !this.$v.email.required && errors.push('E-mail is required')
        return errors
        },
        passwordErrors () {
        const errors = []
        if (!this.$v.password.$dirty) return errors
        !this.$v.password.minLength && errors.push('Password must be minimum of 8 characters')
        !this.$v.password.required && errors.push('Password is required')
        return errors
        },
    },

    methods: {
        // submit () {
        // this.$v.$touch()

        // },
        async registerUser() {
          this.$v.$touch()
          // this.isApierror = false;
          // this.isSuccess = false;
          if (!this.$v.$invalid) {
            const postData = {
            name: this.name,
            email: this.email,
            password: this.password,
            };

            await axios.post("http://localhost:8000/api/register", postData)
              .then(res => {
                  console.log(res);
                  alert('register sucess');
                  this.$router.push({ name: 'Home' })
                  // this.isSuccess = true;
                  // this.isApierror = false;
                  // this.$v.$reset();
                  // this.resetData();
              })
              .catch(err => {
                  // this.errors = err.response.data
                  console.log(err.response.data)
              })      
            }
          }
        },

}
</script>
<style scoped>
/* Google Font Link */
@import 'https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700&display=swap';
* {
  display: inline;
  font-family: "Poppins", sans-serif;
}
.row {
  display: flex;
  justify-content: flex-start;
}
.card{
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  /* position: fixed; */
  background: #ffffff;
  padding: 30px;
}

.container{
  position: relative;
  display: flex;
  justify-content: flex-start;
  max-width: 850px;
  width: 100%;
  background: #fff;
  padding: 30px 30px;
  box-shadow: 0 5px 10px rgba(0,0,0,0.2);
  perspective: 2700px;
}
.f-b{
  height: 100%;
  width: 50%;
  padding: 2em 2em;
  padding-right: 4em;
}
.cover {
  position: absolute;
  top: 0;
  left: 50%;
  height: 100%;
  width: 50%;
}
.backImg{
  position: absolute;
  height: 100%;
  width: 100%;
  object-fit: cover;
  opacity: 0.7;
}
.text{
  position: absolute;
  z-index: 130;
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.text .text-1,
.text .text-2{
  font-size: 26px;
  font-weight: 600;
  color: #fff;
  text-align: center;
}
</style>