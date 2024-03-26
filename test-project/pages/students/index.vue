
<script lang="js">
import { defineComponent } from 'vue';
import  StudentsTable  from "../../components/StudentsTable.vue";

export default defineComponent({
  name: 'Students',
  components: StudentsTable
});

</script>

<template>
<StudentsTable />
</template>

<style scoped>

</style>