<template>
  <div id="app">
    <header>
      <section class="Subject-lessons">
        <h1>{{ sitename }}</h1>

        <div v-if="showProduct">
          <div class="cart-button">
            <button @click="showCheckout">
              {{ this.cart.length }}Checkout
            </button>
          </div>
          <product :products="products" @addProduct="addToCart"></product>
        </div>
        <div v-else>
          <div class="cart-button">
            <button @click="showCheckout">Back home</button>
          </div>
          <checkout :cart="cart" @removeProduct="removeProduct"></checkout>
        </div>
      </section>
    </header>
  </div>
</template>

<script>
import product from "./components/Lessons.vue";
import checkout from "./components/checkoutForm.vue";

export default {
  name: "App",
  components: {
    product,
    checkout,
  },
  data() {
    return {
      sitename: "After school Lesson",
      cart: [],
      products: [],
      showProduct: true,
    };
  },
  created() {
    console.log("requesting data from server ...");
    fetch("https://individual2cw.herokuapp.com/collection/lesson", {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        mode: "no-cors",
      },
    })
      .then((response) => response.json())
      .then((data) => (this.products = data));
  },
  methods: {
    showCheckout() {
      // console.log(this.showProduct);
      this.showProduct = this.showProduct ? false : true;
    },
    removeProduct(product) {
      this.cart.splice(this.cart.indexOf(product), 1);
    },
    addToCart(product) {
      console.log("addLesson event received by the root component.");
      this.cart.push(product);
    },
    cartItemCount() {
      return this.cart.length;
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

header {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: 10px 30px;
  font-size: 25px;
  color: blue;
  font-family: "Helvetica";
}

.cart-head {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: 10px 30px;
  font-size: 25px;
  color: blue;
  font-family: "Helvetica";
}
.Sort {
  top: 300px;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: 10px 30px;
  font-size: 20px;
  color: blue;
  font-family: "
    Montserrat
    ";
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
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  top: 200;
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
  margin-top: 20px;
}
.product-box {
  display: flex;
  flex-grow: 0.5;
  flex-direction: column;
  align-items: center;
  border: 1px solid #f7f7f7;
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
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #ffffff;
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
