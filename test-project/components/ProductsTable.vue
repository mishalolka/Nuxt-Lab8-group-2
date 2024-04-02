<script setup lang="ts">
useHead({
  title: 'Список товарів'
})

const cols = [
  { key: 'title', label: 'Title', sortable: true },
  { key: 'category', label: 'Category', sortable: true},
  { key: 'rating', label: 'Rating', sortable: true },
  { key: 'price', label: 'Price', sortable: true },
  { key: 'brand', label: 'Brand', sortable: true },
  { key: 'thumbnail', label: 'Thumbnail'},
  { key: 'description', label: 'description', sortable: true },
];

const { data } = await useFetch<any>('https://dummyjson.com/products');
const ps = ref(data.value.products);
const q = ref('');
const p = ref(1);
const pCount = 10;
const total = ref(ps.value.length);
const s = ref({ column: '', direction: 'asc' as const })

const sortedRs = computed(() => {
  const { column, direction } = s.value
  const sortedPs = [...ps.value]

  if ( direction && column) {
    sortedPs.sort((a, b) => {
      const bValue= b[column]
      const aValue = a[column]
      if (aValue > bValue) return direction === 'asc' ? 1 : -1
      if (aValue < bValue) return direction === 'asc' ? -1 : 1
      return 0
    })
  }

  return sortedPs
})

const rows = computed(() => {
  let filteredPs = [...sortedRs.value]

  if (q.value) {
    filteredPs = filteredPs.filter(product => {
      return Object.values(product).some(value => {
        return String(value).toLowerCase().includes(q.value.toLowerCase())
      })
    })
  }
  total.value = filteredPs.length;
  const start = (p.value - 1) * pCount
  const end = start + pCount
  return filteredPs.slice(start, end)
})

watch(q,()=>{
  p.value = 1;
})

</script>

<template>
  <div>
    <div class="flex p-3 border-b border-gray-200 justify-center">
      <UInput placeholder="Пошук..." color="black" v-model="q"/>
    </div>
    <UTable class="w-full"
            :ui="{ th: {base: 'text-center'}, td: { base: 'max-w-[0] truncate' } }"
            :columns="cols"
            :rows="rows"
            v-model:sort="s"
            sort-mode="manual"
            sort-asc-icon="i-heroicons-arrow-up-20-solid"
            sort-desc-icon="i-heroicons-arrow-down-20-solid"
            :sort-button="{ icon: 'i-heroicons-sparkles-20-solid', color: 'primary', variant: 'outline', size: '2xs', square: false, ui: { rounded: 'rounded-full' } }"

    >
      <template #thumbnail-data="{ row }">
        <img class="w-[100px] h-[100px]" :src="row.thumbnail" alt="..." />
      </template>
      <template #rating-data="{ row }">
        <span :class="row.rating < 4.5? 'text-red-700' : 'text-green-700' ">{{ row.rating }}</span>
      </template>

    </UTable>
    <div class="flex justify-center mt-5">
      <UPagination v-model="p" :page-count="pCount" :total="total" class="text-black"/>
    </div>
  </div>
</template>