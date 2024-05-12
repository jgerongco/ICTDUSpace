<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header">
        <h4>Reservation</h4>
      </div>
      <div class="card-body">
        <!-- Error messages display -->
        <ul class="alert alert-warning" v-if="Object.keys(this.errorList).length > 0">
          <li class="mb-0 ms-3" v-for="error in errorList" :key="error">
            {{ error[0] }}
          </li>
        </ul>
        <!-- Form fields -->
        <div class="row">
          <!-- Form inputs -->
          <!-- Firstname -->
          <div class="col-12 mb-3">
            <label for="">Firstname</label>
            <input type="text" class="form-control" v-model="model.res.firstname" />
          </div>
          <!-- Lastname -->
          <div class="col-12 mb-3">
            <label for="">Lastname</label>
            <input type="text" class="form-control" v-model="model.res.lastname" />
          </div>
          <!-- Email -->
          <div class="col-12 mb-3">
            <label for="">Email</label>
            <input type="email" class="form-control" v-model="model.res.email" />
          </div>
          <!-- Faculty -->
          <div class="col-12 mb-3">
            <label for="">Faculty</label>
            <input type="text" class="form-control" v-model="model.res.faculty" />
          </div>
          <!-- People -->
          <div class="col-12 mb-3">
            <label for="">People</label>
            <input type="text" class="form-control" v-model="model.res.people" />
          </div>
          <!-- Date -->
          <div class="col-12 mb-3">
            <label for="">Date</label>
            <input type="date" class="form-control" v-model="model.res.date" />
          </div>
          <!-- Purpose -->
          <div class="col-12 mb-3">
            <label for="">Purpose</label>
            <input type="text" class="form-control" v-model="model.res.purpose" />
          </div>
          <!-- Buttons -->
          <div class="col-12 mb-2 text-end">
            <button type="button" @click="saveStudent" class="btn btn-margin">
              Save
            </button>
            <button type="button" @click="Cancel" class="btn btn-margin">
              Cancel
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
          people: "",
          date: "",
          purpose: "",
        },
      },
    };
  },
  methods: {
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
            people: "",
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
    Cancel() {
      this.$router.push("/reservation"); // Redirect to the reservation page
    },
    logout() {
      localStorage.removeItem("token"); // Clear token from local storage
      alert("Logout Successfully");
      this.$router.push("/"); // Redirect to the login page
    },
  },
};
</script>

<style>
.btn-margin {
  margin-right: 10px; /* Adjust as needed */
}
</style>
