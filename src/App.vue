<script>
import AmazingProduct from "./components/AmazingProduct.vue"
import { ref, reactive } from "vue"

export default {
  components: {
    AmazingProduct
  },
  setup() {
    // entry point for composition API
    
    const name = ref("LadyTank Studios")
    // always use const for refs to avoid re-assigning them in setup
    // if forgetting to use .value (since it would re-assign to a non ref)

    console.log(name)
    // runs first
    // note that in setup, we need to use .value of refs

    const custom = reactive({ name: "Orc", price: 5})
    // we don't need to use ref for objects/arrays since they are already
    // accessed by reference
    console.log(custom)
    // note we don't need to use .value when using reactives due to this

    // however, can't re-assign reactives, must operate on their properties

    // can use destructuring with reactives using toRefs function

    const orderProduct = () => {
      alert('Order in process')
    }

    const addItemToCart = (item) => alert(`${item} added to cart`)

    // note: have to return anything from here to access it outside
    return { name, orderProduct, addItemToCart, custom }
  },

  created() {
    console.log(this.name)
    // runs second
    // note that for refs, in created/etc (&templates) we do NOT use .value on refs
  }
}
</script>

<template>
  <h1>{{ name }}</h1>
  <input type="text" v-model="name" />
  <h2>Store</h2>
  <button @click="orderProduct">Order The Product Naow</button>
  <AmazingProduct name="Orc" :price="5" @addToCart="addItemToCart"></AmazingProduct>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
