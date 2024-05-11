<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header">
        <h4>Reservation</h4>
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
            <label for="">Firstname</label>
            <input
              type="text"
              class="form-control"
              v-model="model.res.firstname"
            />
          </div>
          <div class="col-12 mb-3">
            <label for="">Lastname</label>
            <input
              type="text"
              class="form-control"
              v-model="model.res.lastname"
            />
          </div>
          <div class="col-12 mb-3">
            <label for="">Email</label>
            <input
              type="email"
              class="form-control"
              v-model="model.res.email"
            />
          </div>
          <div class="col-12 mb-3">
            <label for="">Faculty</label>
            <input
              type="text"
              class="form-control"
              v-model="model.res.faculty"
            />
          </div>
          <div class="col-12 mb-3">
            <label for="">People</label>
            <input
              type="text"
              class="form-control"
              v-model="model.res.people"
            />
          </div>
          <div class="col-12 mb-3">
            <label for="">Date</label>
            <input
              type="date"
              class="form-control"
              v-model="model.res.date"
            />
          </div>
          <div class="col-12 mb-3">
            <label for="">Purpose</label>
            <input
              type="text"
              class="form-control"
              v-model="model.res.purpose"
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
  name: "reserveCreate",
  data() {
    return {
      errorList: "",
      model: {
        res: {
          firstname: "",
          lastname: "",
          email: "",
          faculty: "",
          people:"",
          date: "",
          purpose: "",
        },
      },
    };
  },

  methods:{
    saveStudent() {
      var mythis = this;
      axios
        .post("http://127.0.0.1:8000/api/reservation", this.model.res)
        .then((res) => {
          console.log(res.data);
          alert(res.data.message);

          this.model.res = {
            firstname: "",
            lastname: "",
            email: "",
            faculty: "",
            people:"",  
            date: "",
            purpose: "",
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

     logout() {
      localStorage.removeItem('token'); // Clear token from local storage
      alert('Logout Successfully');
      this.$router.push('/'); // Redirect to the login page
    },
  },
  
};
</script>
