<template>
<header>
    <div class="wrapper">
      <nav class="navbar navbar-expand-lg bg-body-tertiary">
        <div class="container">
          <!-- <RouterLink class="navbar-brand" to="/">Navbar</RouterLink> -->
          <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <router-link class="nav-link" aria-current="page" to="/admin/home"
                  >Home</router-link
                >
              </li>
              <li class="nav-item">
                <RouterLink class="nav-link" to="/admin/reservation">Student Resrevation</RouterLink>
              </li>
              <li class="nav-item">
                <RouterLink class="nav-link" to="/admin/history">History</RouterLink>
              </li>
              <li class="nav-item">
                <RouterLink class="nav-link" to="/admin/Report">Report</RouterLink>
              </li>
               <li class="nav-item">
                <RouterLink class="nav-link" to="/admin/students">Student</RouterLink>
              </li>
              <!-- <li class="nav-item">
                <router-link class="nav-link" to="/students"
                  >Students</router-link
                >
              </li> -->
              <li class="nav-item">
                 <button class="nav-link" @click="logout">Logout</button>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </div>
  </header>


  <div class="container mt-5">
    <div class="card">
      <div class="card-header">
        <h4>Add Students</h4>
      </div>
      <div class="card-body">
        <ul
          class="alert alert-warning"
          v-if="Object.keys(this.errorList).length > 0"
        >
          <li class="mb-0 ms-3" v-for="error in errorList" :key="error">
            {{ error[0] }}
          </li>
        </ul>
        <div class="row">
          <div class="col-12 mb-3">
            <label for="">Id Number</label>
            <input
              type="text"
              class="form-control"
              v-model="model.student.name"
            />
          </div>
         <div class="col-12 mb-3">
            <label for="courseSelect">Course</label>
            <select id="courseSelect" class="form-control" v-model="model.student.course">
              <option value="">Select a course</option>
              <option value="Course 1">Course 1</option>
              <option value="Course 2">Course 2</option>
              <option value="Course 3">Course 3</option>
              <!-- Add more options as needed -->
            </select>
          </div>
          <div class="col-12 mb-3">
            <label for="">Email</label>
            <input
              type="text"
              class="form-control"
              v-model="model.student.email"
            />
          </div>
          <div class="col-12 mb-3">
            <label for="">Phone</label>
            <input
              type="text"
              class="form-control"
              v-model="model.student.phone"
            />
          </div>
           <div class="col-12 mb-3">
            <label for="">Password</label>
            <input
              type="password"
              class="form-control"
              v-model="model.student.password"
            />
          </div>
          <div class="col-12 mb-3 text-end">
            <button type="button" @click="saveStudent" class="btn btn-success">
              Save
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import axios from "axios";

export default {
  name: "studentCreate",
  data() {
    return {
      errorList: "",
      model: {
        student: {
          name: "",
          course: "",
          email: "",
          phone: "",
          password: "",
        },
      },
    };
  },
  methods: {
    logout() {
      localStorage.removeItem('token'); // Clear token from local storage
      this.$router.push('/admin'); // Redirect to the login page
    },
    saveStudent() {
      var mythis = this;
      axios
        .post("http://127.0.0.1:8000/api/students", this.model.student)
        .then((res) => {
          console.log(res.data);
          alert(res.data.message);

          this.model.student = {
            name: "",
            course: "",
            email: "",
            phone: "",
            password: "",
          };
          this.errorList = "";
        })
        .catch(function (error) {
          if (error.response) {
            if (error.response.status == 422) {
              mythis.errorList = error.response.data.errors;
            }
          } else if (error.request) {
            console.log(error.request);
          } else {
            console.log("Error", error.message);
          }
        });
    },
  },
   logout() {
      localStorage.removeItem('token'); // Clear token from local storage
      alert('Logout Successfully');
      this.$router.push('/'); // Redirect to the login page
    },
};
</script>
