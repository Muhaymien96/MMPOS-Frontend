<template>
  <section class="section_3">
    <div class="container">
      <h2 class="testimonial text-dark pt-3">User Profile</h2>
      <br /><br />
      <div class="row">
        <div class="member member-box col-md-4 col=sm-6 col-xs-12" v-if="users">
          <img
            class="img-member member-box"
            src="https://i.ibb.co/ZTGw6QB/roger-berry-avatar-placeholder-11562991561rbrfzlng6h.png"
          />
          <br />
          <h2 class="name-member name mt-2 text-dark">Name: {{ users.fullname }}</h2>
          <br />
          <h2 class="expertise-member expertise text-dark">
            Email: {{ users.email }}
          </h2>
          <br />
          <h2 class="expertise-member expertise text-dark">
           Contact: {{ users.contact }}
          </h2>
          <br />
          <div class="buttons d-flex">
            <button class="btn btn-danger">Delete</button>
            <button
              type="button"
              class="btn btn-secondary float-start"
              style="margin: 10px"
              data-bs-toggle="modal"
              data-bs-target="#exampleModal1"
            >
              Edit
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Modal for edit  profile -->
  <div
    class="modal fade"
    id="exampleModal1"
    tabindex="-1"
    aria-labelledby="exampleModalLabel1"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Edit User</h5>
          <p>(not working yet)</p>

          <button
            type="button"
            class="btn-close btn-danger"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <form @submit.prevent="updateProduct">
            <ul>
              <li>NAME</li>
              <li><input v-model="name" required type="text" /></li>
              <li>CONTACT</li>
              <li><input v-model="contact" required type="text" /></li>
              <li>EMAIL</li>
              <li><input v-model="email" required type="email" /></li>
            </ul>
            <div class="modal-footer">
              <button
                type="button"
                class="btn btn-secondary"
                data-bs-dismiss="modal"
              >
                Close
              </button>
              <button type="submit" class="btn btn-success">
                Save changes
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      users: null,
      name: "",
      contact: "",
      email: "",
    };
  },
  mounted() {
    if (!localStorage.getItem("jwt")) {
      alert("User not logged in");
      return this.$router.push({ name: "Login" });
    }
    fetch("https://mmpos-group-api.herokuapp.com/users/single-user/", {
      method: "GET",
      headers: {
        "Content-type": "application/json; charset=UTF-8",
        Authorization: `Bearer ${localStorage.getItem("jwt")}`,
      },
    })
      .then((response) => response.json())
      .then((json) => {
        console.log(json);
        this.users = json;
      })
      .catch((err) => {
        alert(err);
      });
  },
};
</script>

<style scoped>
.img-member.member-box {
  height: 150px;
  width: 150px;
  object-fit: cover;
}

h1 {
  text-align: center;
  margin: 1em auto;
  color: #344055;
}

.member {
  margin-top: 70px !important;
  background-image: linear-gradient(
    to top,
    rgba(236, 234, 235, 0.79) 0%,
    rgba(255, 255, 255, 0.72) 100%
  );
  background: #9f9f9f;
  width: 500px;
  height: 380px;
  border-radius: 7px;
  margin: auto;
  margin-bottom: 50px;
  text-align: center;
  padding: 20px 10px;
  position: relative;
  top: 0;
  left: 0;
}

.member .img-member {
  border-radius: 50%;
  margin-top: -80px;
  border: 1px solid black;
  background-color: lightgray;
}

.member .name-member {
  color: #344055;
  margin: 7px 0 7px 0;
}

.member .expertise-member {
  color: #888098;
  margin-top: 0;
  margin: 7px 0 7px 0;
  font-size: 20px;
  font-weight: 500;
}
</style>
