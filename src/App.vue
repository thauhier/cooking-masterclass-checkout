<template>
  <div id="app">
    <h1>Course Shop</h1>
    <CourseList :courses="products" @add-course="addToCart" />
    <Cart :items="cart" @remove-course="removeFromCart" />
  </div>
</template>

<script>
import { reactive, watch, onMounted } from 'vue'
import CourseList from './components/CourseList.vue'
import Cart from './components/Cart.vue'

export default {
  name: "App",
  components: { CourseList, Cart },
  setup() {
    const products = reactive([
      { id:1, name:"Spaghetti", description:"Classic Italian Pasta with rich meat sauce.", chef:"Gordan Ramsey", level:"*****", price:165.00, available:"", image:"https://www.servingdumplings.com/wp-content/uploads/2023/01/the-best-spicy-spaghetti-bolognese-4-75b75f26.jpg" },
      { id:2, name:"Croissant", chef:"Ratatouille", level:"**", price:80.00, description:"Nicely sized croissant with chocolate spread inside", available:"SOLD OUT", image:"https://www.theflavorbender.com/wp-content/uploads/2020/05/French-Croissants-SM-2363.jpg" },
      { id:3, name:"Chicken Soup", chef:"Thauhier", level:"*", price:120.00, description:"Nice and warm Chicken Soup fresh.", available:"", image:"https://theforkedspoon.com/wp-content/uploads/2019/12/Chicken-Soup-6-1.jpg" },
      { id:4, name:"Briyani", chef:"Random Indian guy", level:"***", price:145.00, description:"Freshly cooked Briyani", available:"SOLD OUT", image:"https://i.pinimg.com/originals/aa/a9/2a/aaa92a3c0a605671a2e1b20871913c34.jpg" },
      { id:5, name:"Chocolate Cake", chef:"Cake Boss", level:"*****", price:225.00, description:"Best cake baked by the best Baker", available:"", image:"https://www.bunsenburnerbakery.com/wp-content/uploads/2023/09/best-chocolate-layer-cake-41.jpg" },
      { id:6, name:"Mac and Cheese", chef:"Gordan Ramsey", level:"*****", price:200.00, description:"Macaroni coated with the most flavourable cheese.", available:"", image:"https://www.allrecipes.com/thmb/e8uotDI18ieXNBY0KpmtGKbxMRM=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/238691-Simple-Macaroni-And-Cheese-mfs_008-4x3-6ed91ba87a1344558aacc0f9ef0f4b41.jpg" }
    ])

    const cart = reactive([])

    // Load persisted cart
    onMounted(() => {
      const saved = localStorage.getItem('cart')
      if (saved) {
        const parsed = JSON.parse(saved)
        parsed.forEach(item => cart.push(item))
      }
    })

    // Persist cart whenever it changes
    watch(
      cart,
      (newCart) => {
        localStorage.setItem('cart', JSON.stringify(newCart))
      },
      { deep: true }
    )

    function addToCart(course) {
      const existing = cart.find(i => i.id === course.id)
      if (existing) {
        existing.qty++
      } else {
        cart.push({ ...course, qty: 1 })
      }
    }

    function removeFromCart(id) {
      const idx = cart.findIndex(i => i.id === id)
      if (idx > -1) cart.splice(idx, 1)
    }

    return { products, cart, addToCart, removeFromCart }
  }
}
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  padding: 20px;
}
</style>