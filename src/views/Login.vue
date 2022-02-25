<template>
  <div>
  <nav-bar />
  <div class="card">
  <div class="container">
    <div class="cover back">
        <img class="backImg" src="https://i.pinimg.com/originals/2d/0b/35/2d0b351df98ed785b8a61a9374446a81.jpg" alt="background" />
        <div class="text">
          <span class="text-1">Every new friend is a <br> new adventure</span>
          <span class="text-2">Let's get connected</span>
        </div>
    </div>
    <div class="f-b">
    <form>
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
        @click="submit"
      >
      Log in
      </v-btn>
      <div class="row signup">
        <span>Don't have an account? </span><br>
        <router-link to="/signup">
        <label>Signup now</label>
        </router-link>
      </div>
    </form>
    </div>
  </div>
  </div>
  <Footer />
  </div>
</template>

<script>
import NavBar from '../components/NavBar.vue'
import Footer from '../components/Footer.vue'
import { validationMixin } from 'vuelidate'
import { required, email } from 'vuelidate/lib/validators'

export default {
  name: 'LogIn',
  mixins: [validationMixin],
  components: {
    NavBar,
    Footer
  },
    validations: {
        email: { required, email },
        password: { required }
    },

    data: () => ({
        email: '',
        password: ''
    }),

    computed: {
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
        // !this.$v.password.minLength && errors.push('Password must be minimum of 8 characters')
        !this.$v.password.required && errors.push('Password is required')
        return errors
        },
    },

    methods: {
        submit () {
        this.$v.$touch()
        },
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
  justify-content: flex-end;
  max-width: 850px;
  width: 100%;
  background: #fff;
  padding: 30px 30px;
  box-shadow: 0 5px 10px rgba(0,0,0,0.2);
  perspective: 2700px;
}
.cover {
  position: absolute;
  top: 0;
  right: 50%;
  height: 100%;
  width: 50%;
}
.f-b{
  height: 100%;
  width: 50%;
  padding: 2em 2em;
  padding-left: 3em;
}
.signup{
  /* width: 50%; */
  height: 100%;
  display: flex;
  justify-content: center;
  align-self: center;
  text-align: center;
  padding: 2em;
}
label{
  color: #9FA8DA;
  cursor: pointer;
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