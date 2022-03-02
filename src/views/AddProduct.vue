<template>
  <div class="products">
    <nav class="navbar navbar-expand-lg navbar-light bg-dark fixed-top">
      <div class="container-fluid">
        <h1 style="margin-right: 50px">PRODUCTS</h1>
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
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <!-- Button trigger modal for add product -->
              <a
                class="nav-link"
                style="cursor: pointer"
                data-bs-toggle="modal"
                data-bs-target="#exampleModal"
              >
                Add a product
              </a>
            </li>
                    
            <li class="nav-item dropdown">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                id="navbarDropdown"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
              >
                Sort by
              </a>
              <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                <li><button class="droppie">Price</button></li>
                <li><hr class="dropdown-divider" /></li>
                <li><button class="droppie">Name</button></li>
              </ul>
            </li>
            <li class="nav-item dropdown">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                id="navbarDropdown1"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
              >
                Catergory
              </a>
              <ul class="dropdown-menu" aria-labelledby="navbarDropdown1">
                <li><button class="droppie">Shoes</button></li>
                <li><hr class="dropdown-divider" /></li>
                <li><button class="droppie">Accessories</button></li>
                <li><hr class="dropdown-divider" /></li>
                <li><button class="droppie">Clothing</button></li>
              </ul>
            </li>
          </ul>
          <!-- <router-link class="nav-link" to="/add">ADD A PRODUCT</router-link> -->
          <router-link class="nav-link" to="/cart">CART</router-link>
          <router-link class="nav-link" to="/profile">PROFILE</router-link>
          <router-link class="nav-link" to="/">LOG OUT</router-link>
        </div>
      </div>
    </nav>

    <!-- Modal for add  product -->
    <div
      class="modal fade"
      id="exampleModal"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Add Nike</h5>

            <button
              type="button"
              class="btn-close btn-danger"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <form @submit.prevent="createProduct">
              <ul>
                <li>NAME</li>
                <li><input v-model="name" required type="text" /></li>
                <li>PRICE</li>
                <li><input v-model="price" required type="number" /></li>
                <li>IMAGE URL</li>
                <li><input v-model="img" required type="text" /></li>
                <label for="genre">CATEGORY:</label>
                <select id="genre" v-model="category" name="genre">
                  <option value="Shoes">Shoes</option>
                  <option value="Accessories">Accessories</option>
                  <option value="Clothing">Clothing</option>
                </select>
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

    <!-- Modal for edit  product -->
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
            <h5 class="modal-title" id="exampleModalLabel">EDIT NIKE</h5>

            <button
              type="button"
              class="btn-close btn-danger"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <form action="">
              <ul>
                <li>NAME</li>
                <li><input v-model="name" required type="text" /></li>
                <li>PRICE</li>
                <li><input v-model="price" required type="number" /></li>
                <li>IMAGE URL</li>
                <li><input v-model="img" required type="text" /></li>
                <li>
                  Shoes<input
                    v-model="category"
                    style="margin: 10px"
                    type="radio"
                  />Accessories<input
                    v-model="category"
                    style="margin: 10px"
                    type="radio"
                  />Clothing<input
                    v-model="category"
                    style="margin: 10px"
                    type="radio"
                  />
                </li>
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

    <div class="container">
      <div class="row">
        <div
          v-for="product of products"
          :key="product.name"
          class="card col-lg-3"
        >
          <img :src="product.img" alt="pik" class="pic" />
          <h3>{{ product.name }}</h3>
          <p>R{{ product.price }}</p>
          <p>{{ product.category }}</p>
          <button type="button" class="btn btn-danger" style="margin: 10px">
            DELETE
          </button>
          <button
            type="button"
            class="btn btn-secondary"
            style="margin: 10px"
            data-bs-toggle="modal"
            data-bs-target="#exampleModal1"
          >
            EDIT
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
