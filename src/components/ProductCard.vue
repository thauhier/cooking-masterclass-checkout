<template>
   <!-- div for product cards -->
    <div class="product-card">
        <img :src="product.image" alt="Image of product on catalgue." class="product-image"/>

        <!-- the product card template -->
        <div class="product-info">
            <h3>{{ product.name }}</h3>
            <p class="descript">{{ product.description }}</p>
            <p class="chef">Chef: {{ product.chef + " " +product.level}}</p>
            <p class="price">R{{ product.price}}</p>
            <p class="availability">{{ product.available }}</p>
        </div>
        <button @click="$emit('toggle-save', product.id)">
            {{ saved ? 'saved':'save'  }}
        </button>
    </div>
</template>

<script>
export default{
    name: "ProductCard",
    props:{
        product:{
        type:Object,
        required:true,},
        saved:{type:Boolean,default:false}
        
    },
}
</script>

<style scoped>
.product-card{
    border: 1px solid #ddd;
    border-radius:8px;
    padding: 10px;
    width:30%;
    background-color:#fff;
    box-shadow:0 2px 6px rgba(0,0,0,0.1);
    position:relative;
    height:450px
}

.product-image{
    width: 100%;
    height:225px;
    object-fit:cover;
    border-radius:6px
}

.product-info{
    margin: 10px;
}

.price{
    font-size: larger;
    font-weight:bold;
    color: #e67e22;
    position:absolute;
    bottom:-10px
}

button{
    padding:8px 12px;
    border: none;
    border-radius:4px;
    cursor:pointer;
    background: #3498db;
    color: white;
    position:absolute;
    right:5px;
    bottom:10px
}
button.saved{
    background: #2ecc71;

}

.descript{
    margin:5px;
    color:grey;
    text-align:center;
    position:absolute;
    bottom:70px
}
.chef{
    margin:5px;
    color:grey;
    text-align:center;
    position:absolute;
    bottom:100px
}
.availability{
    position: absolute;
    color:red;
    font-family:bold;
    right:0;
    bottom:30%;
}
</style>