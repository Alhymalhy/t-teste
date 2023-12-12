<script setup lang="ts">
import items from '@/assets/items.json'
import materials from '@/assets/materials.json'

const sortOptions = [
  { id: 0, name: 'Цена по возрастанию' },
  { id: 1, name: 'Цена по убыванию' },
]

const selectedSortId = shallowRef(0)
const selectedMaterialId = shallowRef(1)

const products = computed(() =>
  items.filter(item => Number(item.material) === Number(selectedMaterialId.value))
    .sort((a, b) =>
      Number(selectedSortId.value) === 0 ? a.price.current_price - b.price.current_price : b.price.current_price - a.price.current_price,
    ),
)
</script>

<template>
  <div class="mx-auto flex flex-col container">
    <h2 class="mb-32px text-36px font-600">
      Комплекты стеллажных систем
    </h2>
    <div class="mb-40px flex gap-24px">
      <CustomSelect v-model="selectedSortId" label="Сортировать по:" :options="sortOptions" />
      <CustomSelect v-model="selectedMaterialId" label="Материал" :options="materials" />
    </div>
  </div>
  <div
    class="grid auto-rows-auto mx-auto place-content-between gap-[49px] container"
  >
    <ProductCard
      v-for="product in products"
      :key="product.id"
      :product="product"
    />
  </div>
</template>

<style>
.container {
  display: flex;
  width: 1920px;
  flex-wrap: wrap;
}
</style>
