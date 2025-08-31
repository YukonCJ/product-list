<template>
  <!-- 購物車區 -->
  <div class="col-md-4">
    <h2 class="mb-3">購物車</h2>
    <div v-if="carts.length === 0">
      <p class="text-muted">購物車目前沒有商品</p>
    </div>
    <ul class="list-group mb-3">
      <li
        v-for="cart in carts"
        :key="cart.id"
        class="list-group-item d-flex justify-content-between align-items-center"
      >
        <div>
          <h6 class="my-0">{{ cart.name }}</h6>
          <small class="text-muted">數量：{{ cart.quantity }}</small>
        </div>
        <div>
          <span class="text-muted">${{ cart.quantity * cart.price }}</span>
          <button class="btn btn-sm btn-outline-danger ms-2" @click="handleRemoveCart(cart)">移除</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { defineProps, defineEmits, inject } from 'vue'
const props = defineProps({
  carts: {
    type: Array,
    required: true,
  },
})

const emit = defineEmits(['remove-cart'])
const handleRemoveCart = (product) => {
  emit('remove-cart', product)
  showNotification(`${product.name} 已從購物車移除`)
}

const showNotification = inject('showNotification')
</script>