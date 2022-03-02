<template>
   <section class="section_proj">
    <div class="container">
      
      <header class="buttons">
        <!-- go to cart -->
        <a href="/cart" id="cart"><svg xmlns="http://www.w3.org/2000/svg" width="34" height="34" fill="currentColor" class="bi bi-bag-fill" viewBox="0 0 16 16">
  <path d="M8 1a2.5 2.5 0 0 1 2.5 2.5V4h-5v-.5A2.5 2.5 0 0 1 8 1zm3.5 3v-.5a3.5 3.5 0 1 0-7 0V4H1v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V4h-3.5z"/>
</svg></a>
  <!-- Button trigger modal for add product -->
              <a
                class="nav-link"
                style="cursor: pointer"
                data-bs-toggle="modal"
                data-bs-target="#exampleModal"
              >
                Add a product
              </a>
</header>
      

<!-- modals -->

<!-- product display -->
      <h2 class="head d-flex justify-content-center text-dark my-5">PRODUCTS</h2>
      <div class="row">
        <div
          class="card col-md-4 col-sm-6 col-xs-12"
          v-for="product in products"
          :key="product.id"
        >
          <div class="imgBx">
            <img
              class="prod-img"
              :src="product.img"
            />
          </div>
          <div class="contentBx">
            <h4>{{ product.title }}</h4>
            <div class="info">
              <div class="desc text-dark">{{ product.description }}</div>
              <div class="category text-dark">{{ product.category }}</div>
              <div class="price text-dark">R {{ product.price }}</div>
             <br>
               <div class="cart d-flex">
            <input type="number" class="form-control" value=1 min=1 id="addToCart${position}">
            <button type="button" class="btn btn-mute ms-3" onclick="addToCart(${position})"><i class="fas fa-shopping-bag fa-1x"></i></button>
          </div>
              </div>
            </div>
        </div>
      </div>
      <br />
    </div>
    <br />
  </section>
</template>
<script>
export default {
  data() {
    return {
      products: null,
        title:"",
      description: "",
      category:"",
      price:"",
      img:""
    };
  },
  // fetching product
  created() {
    if (localStorage.getItem("jwt")) {
      fetch("https://mmpos-group-api.herokuapp.com/products", {
        method: "GET",
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          this.products = json;
          this.products.forEach(async (product) => {
            await fetch(
              "https://mmpos-group-api.herokuapp.com/products/" + product.title,
              {
                method: "GET",
                headers: {
                  "Content-type": "application/json; charset=UTF-8",
                  Authorization: `Bearer ${localStorage.getItem("jwt")}`,
                },
              }
            )
              .then((response) => response.json())
              .then((json) => {
                product.author = json.title;
              });
          });
        })
        .catch((err) => {
          alert("Log in failed");
        });
    } else {
      alert("Not logged in");
      this.$router.push({ name: "Login" });
    }  
  },
   methods: {
    createProduct() {
      if (!localStorage.getItem("jwt")) {
        alert("User not logged in");
        return this.$router.push({ name: "Login" });
      }
      fetch("https://mmpos-group-api.herokuapp.com/products", {
        method: "POST",
        body: JSON.stringify({
          name: this.name,
          category: this.category,
          price: this.price,
          img: this.img,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          alert("Product Created");
          this.$router.push({ name: "Products" });
        })
        .catch((err) => {
          alert(err);
        });
    },
  }
   
};
</script>
<style scoped>
* {
  box-sizing: border-box;
}
.head{
  letter-spacing: 6px;
  text-align: center;
  transform: scale(.95, 1);
  color: #111 !important;
}
.section_proj {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: white;
}
.price{
  font-weight: 500 !important;
  margin-bottom: 12px !important;
}


.container .card {
  /* position: relative; */
 margin-right: 40px !important;
 margin-left: 40px !important;
 margin-top: 20px !important;
  width: 280px;
  height: 450px;
  background: rgb(221, 200, 200);
  border-radius: 20px;
  overflow: hidden;
  
}
.button1 {
  background-color: transparent !important;
  margin-left: 10px;
  float: left;
  font-size: 30px !important;
}
.button2 {
  background-color: transparent !important;
  margin-right: 10px;
  float: right;
  font-size: 30px !important;
}

.container .card:before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: #f8ad9d;
  clip-path: circle(150px at 80% 20%);
  transition: 0.5s ease-in-out !important;
}

.container .card:hover:before {
  clip-path: circle(300px at 80% -20%);
}

.container .card .imgBx {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 10000;
  width: 100%;
  height: 220px;
  transition: 0.5s;
  margin-right: 50px !important;
}

.container .card:hover .imgBx {
  top: 0%;
  transform: translateY(0%);
}
.cart{
  top: -50% !important;
}

.container .card .imgBx img {
  position: absolute;
  top: 50%;
  left: 47%;
  transform: translate(-50%, -50%);
  width: 190px;
  height: 200px;
  object-fit:inherit;
}

.prod-img{
  -webkit-border-radius: 30px;
-moz-border-radius: 30px;
border-radius: 30px;
transition-delay: 0.4s;
}

.container .card .contentBx {
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 120px;
  text-align: center;
  transition: 1s;
  z-index: 10;
  padding-right: 25px !important;
}

.container .card:hover .contentBx {
  height: 210px;
}

.container .card .contentBx h4 {
  position: relative;
  font-weight: 500;
  letter-spacing: 1px;
  color: #fff;
  margin: 0;
}

.container .card .contentBx .size,
.container .card .contentBx .color {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 8px 20px;
  transition: 0.3s;
  opacity: 0;
  visibility: hidden;
  padding-top: 0;
  padding-bottom: 0;
}

.container .card:hover .contentBx .size {
  opacity: 1;
  visibility: visible;
  transition-delay: 0.3s;
}

.container .card:hover .contentBx .color {
  opacity: 1;
  visibility: visible;
  transition-delay: 0.3s;
}

.container .card .contentBx .size h3,
.container .card .contentBx .color h3 {
  font-weight: 300;
  font-size: 14px;
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-right: 10px;
}

.container .card .contentBx .size span {
  width: 26px;
  height: 26px;
  text-align: center;
  line-height: 26px;
  font-size: 14px;
  display: inline-block;
  color: #111;

  margin: 0 5px;
  transition: 0.3s;
  color: #111;
  border-radius: 4px;
  cursor: pointer;
}

.container .card .contentBx a {
  display: inline-block;
  padding: 10px 20px;
  background: #fff;
  border-radius: 4px;
  margin-top: 10px;
  text-decoration: none;
  font-weight: 600;
  color: #111;
  opacity: 0;
  transform: translateY(50px);
  transition: 0.3s;
  margin-top: 0;
}

.container .card:hover .contentBx a {
  opacity: 1;
  transform: translateY(0px);
  transition-delay: 0.3s;
}

#cart {
  float: right;
  margin-top: 30px;
  margin-right: -50px;
}
@media (max-width: 500px){
  .section_proj {
 width: 112%;
}
}
</style>
