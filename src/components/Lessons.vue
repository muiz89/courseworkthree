<template>
  <section class="Suject-lessons">
    <div class="product-container" id="Shop-product">
      <div v-for="product in products.slice(0, 8)" :key="product.id">
        <div class="product-container" id="Shop-product">
          <div class="product-box">
            <h2 v-text="product.Subject"></h2>
            <div class="product-img">
              <figure>
                <img v-bind:src="product.image" />
              </figure>
            </div>
            <div class="product-details">
              <p v-html="product.Location"></p>
              <p>Price: {{ product.price }}</p>
              <p>Spaces: {{ product.availableInventory }}
              <div class="add-cart">
                <button v-on:click="addToCart(product)">ADD TO CART</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "LessonList",
  props: ["products"],

  methods: {
    addToCart(product) {
      console.log("Added lesson", product.id);
      product.availableInventory -= 1
      this.$emit("addProduct", product);
    },
    canAddToCart(product) {
    return product.spaces > 0;
    },
    fetchlessons() {
      //fetching the lessons from server
      fetch("https://individual2cw.herokuapp.com/collection/lesson").then(
        function (response) {
          response.json().then(function (json) {
            return json;
            });
            }
            );
            },
            },
  };
</script>
<style scoped>
body {
  width: 100%;
}
html {
  scroll-behavior: smooth;
}

.cart-head {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: 40px 50px;
  font-size: 25px;
  color: blue;
  font-family: "Helvetica";
}

.classes-back button {
  width: 170px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: blue;
  letter-spacing: 2px;
  margin-top: 10px;
  margin-left: 1200px;
  border-radius: 10%;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 2px 2px 30px rgba(0, 0, 0, 0.1);
  animation: fade 0.9s;
}

.Subject-lessons {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.product-container {
  margin-top: 0px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  top: 500px;
}
.product-container h2 {
  font-size: 30px;
  color: blue;
  font-family: "Helvetica";
}
#Shop-product {
  width: 90%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  margin-top: 10px;
}
.product-box {
  display: flex;
  flex-grow: 0.5;
  flex-direction: column;
  align-items: center;
  border: 5px solid #f7f7f7;
  border-radius: 20px;
  margin: 30px;
}
.product-img {
  width: 200px;
  height: 210px;
  margin: 20px;
  cursor: pointer;
  position: relative;
}
.product-img img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  object-position: center;
}
.product-details {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  padding: 10px 20px;
  border-top: 1px solid #f3f3f3;
}
.add-cart button {
  width: 170px;
  font-size: 10px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: white;
  letter-spacing: 2px;
  margin-top: 14px;
  border-radius: 10%;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 2px 2px 30px rgba(0, 0, 0, 0.1);
  animation: fade 0.9s;
}
.cart-button button {
  width: 170px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #ffffff;
  letter-spacing: 2px;
  margin-top: 10px;
  margin-left: 1200px;
  border-radius: 10%;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 2px 2px 30px rgba(0, 0, 0, 0.1);
  animation: fade 0.9s;
}
.CheckOut-form {
  display: flex;
  flex-direction: row;
  margin-top: 100px;
  width: 1000px;
  height: 70px;
  margin-left: 150px;
  border: 1px solid #f1f1f1;
  padding: 20px;
  background-color: white;
}
.CheckOut-form input {
  width: 90%;
  padding: 15px;
  margin: 5px 0 22px 0;
  display: inline-block;
  border: none;
  background: #f1f1f1;
}
.CheckOut-form button {
  background-color: blue;
  color: white;
  padding: 16px 20px;
  margin: 8px 0;
  border: 1;
  cursor: pointer;
  width: 100%;
  opacity: 0.9;
}
</style>
