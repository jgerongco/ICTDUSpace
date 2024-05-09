<template>
    <div class="container">
        <div class="row justify-content-center mt-5">
            <div class="col-md-6">
                <div class="card">
                    <div class="card-header bg-primary text-white">
                        <h3 class="card-title text-center">Student Login</h3>
                    </div>
                    <div class="card-body">
                         <form @submit.prevent="login">
                            <div class="mb-3">
                                <label for="email" class="form-label">Email</label>
                                <input type="email" class="form-control" v-model="email" id="email" name="email" required>
                            </div>
                            <div class="mb-3">
                                <label for="password" class="form-label">Password</label>
                                <input type="password" v-model="password" class="form-control" id="password" name="password" required>
                            </div>
                            <button type="submit" class="btn btn-primary btn-block">Login</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      email: '',
      password: ''
    };
  },
  methods: {
    async login() {
      try {
        const response = await axios.post('http://127.0.0.1:8000/api/studentlogin', {
          email: this.email,
          password: this.password
        });
        
        const token = response.data.token;
        localStorage.setItem('token', token); // Store token in localStorage

         this.$router.push('/home');
        // Redirect or perform other actions upon successful login
      } catch (error) {
        alert('Unauthorized');
        console.error(error);

        // Handle login error
      }
    }
  }
};
</script>

<style scope>

h2{
  background-color: #f5bfc1;
  color: #901430;
}

</style>