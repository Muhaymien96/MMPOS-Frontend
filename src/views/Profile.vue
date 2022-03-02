<template>
  <h1 class="mt-4">User Profile</h1>
<div class="Profile">
  <div class="row">
    <h4 class="mb-4">User Information</h4>
    <div class="col-sm-6">
      <svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" fill="#f8ad9d" class="bi bi-person-square my-2" viewBox="0 0 16 16">
  <path d="M11 6a3 3 0 1 1-6 0 3 3 0 0 1 6 0z"/>
  <path d="M2 0a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2H2zm12 1a1 1 0 0 1 1 1v12a1 1 0 0 1-1 1v-1c0-1-1-4-6-4s-6 3-6 4v1a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1h12z"/>
</svg>
    </div>
    <div class="col-sm-6">
      <p class="text-dark">Name : {{name}}</p>
      <p class="text-dark">Email : {{email}}</p>
      <p class="text-dark">Contact Number : {{contact}}</p>
      <!-- <p class="text-dark">Password : {{password}}</p> -->
    </div>
  </div>
</div>
  <a href="/products" class="back-to-shop btn btn my-5">Back To Shopping</a>

</template>

<script>
export default {
  data() {
    return {
      name: "",
       email: "",
       contact: "",
      //  password: "",
    };
  },
   methods: {
    register() {
      fetch("https://mmpos-group-api.herokuapp.com/users/" + this.$route.params.id, {
        method: "GET",
        body: JSON.stringify({
          name: this.fullname,
          email: this.email,
          contact: this.contact,
          // password: this.password,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then((response) => response.json())
        .then((json) => {
          alert("User Data Retrieved");
          localStorage.setItem("jwt", json.jwt);
        })
        .catch((err) => {
          alert(err);
        });
    },
  },
};

</script>

<style scoped>
.Profile {
  border: 1px solid black;
  border-radius: 10px;
  width: 60%;
  margin-top: 50px;
  margin-inline: auto;
  padding: 40px;
}

.col-sm-6 p{
  text-align: initial;
  border-bottom: 1px solid #000;
  width: 75%;
}

.back-to-shop {
  text-decoration: none;
  background: #f8ad9d;
  padding: 10px;
  border-radius: 5px;
}

.back-to-shop:hover {
  background: #f4978e;
}

</style>