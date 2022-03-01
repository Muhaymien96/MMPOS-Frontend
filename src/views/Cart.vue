<template>
		<div class="wrapper" v-show="isActive">
      <div class="row">
          <div class="col" v-for="product in products" :key="product.id">
            <div class="card" >
				<div class="card-spaceBeet"> <span>{{product.title}}</span> <span @click="addBasket(product)">Ekle</span> </div>
				<div class="card-spaceBeet"> <span> {{product.price}} TL </span> <span> {{item.amount}} Adet </span> </div>
			</div>
          </div>
      </div>
			
		
		<h3>Sepetim</h3>
    <h4 v-show="baskets.length <= 0">Sepetinizde Henüz Ürün Bulunmamaktadır.</h4>
		<ul>
			<li v-for="(item, index) in baskets" :key="index">
				{{item.title}} - <span> {{item.price}} TL </span> - <span @click="deleteProduct(index, item)">Sil</span>
			</li>
		</ul>
		<p style="text-align:right; margin-right:15px;">Total: {{totalPrice}} TL</p>
      </div>
</template>

<script>
	export default {
    name: "Cart",
    data() {
      return {
        baskets:[],
      };
    },
    mounted() {
    fetch("https://mmpos-group-api.herokuapp.com/products/" + this.id, {
      method: "GET",
      headers: {
        "Content-type": "application/json; charset=UTF-8",
        Authorization: `Bearer ${localStorage.getItem("jwt")}`,
      },
    })
      .then((response) => response.json())
      .then(async (json) => {
        this.blog = json;
        await fetch(
          "https://mmpos-group-api.herokuapp.com/users/" + json.author,
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
            this.blog.author_name = json.name;
          });
      });
  },
    methods:{
      addBasket(value){
        var item = this.items.find(x=> x.id == value.id);
        if(user.cart.length <= 0){
          window.alert('Could not find product')
        }
        else{
          this.baskets.push(value);
          item.amount -=1;
        }
        
      },
      deleteProduct(index, item){
        var item = this.items.find(x=> x.id == item.id);
        item.amount +=1;
        this.baskets.splice(index,1);
      }
    },
    computed:{
      totalPrice(){
         let total = 0;
      this.baskets.forEach(element => {
        total += Number(element.price);
      });
      return total;
      }
    }
  };
</script>
<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600&display=swap');
	* {
		box-sizing: border-box;
		margin: 0;
		padding: 0;
	}
  body{
    font-family: 'Poppins', sans-serif;
    font-size:14px;
  }
  .row {
  position: relative;
  display: flex;
  flex-wrap: wrap;
}
.col {
  position: relative;
  max-width: 100%;
  padding-left: 15px;
  padding-right: 15px;
  margin-bottom: 10px;
  flex-basis: 0;
  flex-grow: 1;
}
	.wrapper {
		position: relative;
		width: 96%;
    max-width:1420px;
    margin:0px auto;
	}

	button {
		position: relative;
		display: inline-block;
		border: none;
    margin:10px;
		padding: 7px 14px;
		font-weight: bold;
		background-color: rgb(86, 222, 246);
		color: #fff;
    cursor:pointer;
	}

	.card {
		position: relative;
		width: 100%;
		height: 150px;
		padding: 10px 17px;
		margin: 0;
		background-color: rgb(207, 246, 243);
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	.card-spaceBeet {
		position: relative;
		width: 100%;
		display: flex;
		justify-content: space-between;
	}


</style>