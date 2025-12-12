<template>
  <section class="cart">
    <h2>Your Cart</h2>
    <div v-if="items.length === 0">Cart is empty</div>
    <div v-else>
      <div v-for="item in items" :key="item.id" class="cart-item">
        <span>{{ item.name }} (R{{ item.price }})</span>
        <input type="number" min="0" v-model.number="item.qty" />
        <button @click="$emit('remove-course', item.id)">Remove</button>
      </div>
      <hr />
      <p>Subtotal: R{{ subtotal }}</p>
      <p>Tax: R{{ tax }}</p>
      <p><strong>Total: R{{ total }}</strong></p>
    </div>
  </section>
</template>

<script>
import { computed } from 'vue'

export default {
  name: "Cart",
  props: {
    items: { type: Array, required: true }
  },
  setup(props) {
    const subtotal = computed(() =>
      props.items.reduce((sum, i) => sum + i.price * i.qty, 0)
    )
    const tax = computed(() => Math.round(subtotal.value * 0.15))
    const total = computed(() => subtotal.value + tax.value)

    return { subtotal, tax, total }
  }
}
</script>

<style scoped>
.cart-item {
  display: flex;
  gap: 8px;
  align-items: center;
  margin-bottom: 8px;
}
input { width: 50px; }
button {
  padding: 4px 8px;
  border: none;
  border-radius: 4px;
  background: #e74c3c;
  color: white;
  cursor: pointer;
}
</style>