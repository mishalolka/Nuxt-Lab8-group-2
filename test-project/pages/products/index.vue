<script lang="js">
import { defineComponent } from 'vue';
import ProductsTable from "~/components/ProductsTable.vue";
export default defineComponent({
  name: 'Products',
  components: ProductsTable
});
</script>

<template>
<ProductsTable />
</template>



<style scoped>

</style>