<template>
  <section class="catalog">
    <h2>Catalogue</h2>
    <div class="catalog-grid">
      <div v-for="course in courses" :key="course.id" class="product-card">
        <img :src="course.image" alt="Image of product" class="product-image"/>

        <div class="product-info">
          <h3>{{ course.name }}</h3>
          <p class="descript">{{ course.description }}</p>
          <p class="chef">Chef: {{ course.chef }} {{ course.level }}</p>
          <p class="price">R{{ course.price }}</p>
          <p class="availability" v-if="course.available === 'SOLD OUT'">Sold Out</p>
        </div>

        <button 
          :disabled="course.available === 'SOLD OUT'" 
          @click="$emit('add-course', course)"
        >
          {{ course.available === 'SOLD OUT' ? 'Sold Out' : 'Add to Cart' }}
        </button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "CourseList",
  props: {
    courses: { type: Array, required: true }
  }
}
</script>

<style scoped>
.catalog-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 12px;
}
.product-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 10px;
  background-color: #fff;
  box-shadow: 0 2px 6px rgba(0,0,0,0.1);
  position: relative;
}
.product-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 6px;
}
.product-info { margin: 10px; }
.price { font-weight: bold; color: #e67e22; }
button {
  padding: 8px 12px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  background: #3498db;
  color: white;
  margin-top: 10px;
}
button:disabled { background: #aaa; cursor: not-allowed; }
.availability { color: red; font-weight: bold; }
</style>