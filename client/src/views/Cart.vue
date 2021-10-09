<template>
  <BasicLayouts>
    <h1>Carrito</h1>
    <table class="ui celled table" v-if="products">
      <thead>
        <tr>
          <th>Producto</th>
          <th>Cantidad</th>
          <th>Precio</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{ product.name }}</td>
          <td>{{ product.quantity }}</td>
          <td>{{ product.price }} $</td>
          <td style="text-align: center">
            <i class="close icon"></i>
          </td>
        </tr>
        <tr>
          <td></td>
          <td>Total:</td>
          <td colspan="2">{{ total }}$</td>
        </tr>
      </tbody>
    </table>

    <button class="ui button primary fluid">
      Generar pedido
    </button>

    <h3 v-if="!products">No tienes productos en el carrito</h3>
  </BasicLayouts>
</template>

<script>
import { onMounted, ref } from 'vue';
import BasicLayouts from '../layouts/BasicLayouts.vue';
import { getProductsCartApi } from '../api/cart';

export default {
  name: 'Cart',
  components: {
    BasicLayouts,
  },
  setup() {
    let products = ref(null);

    onMounted(async () => {
      const response = await getProductsCartApi();
      products.value = response;
    });

    return {
      products,
    };
  },
};
</script>

<style></style>
