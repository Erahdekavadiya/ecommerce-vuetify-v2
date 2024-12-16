<template>
  <v-card>
    <v-card-title>Filter</v-card-title>
    <v-card-text>
      <!-- Category Dropdown -->
      <v-select
        label="Category"
        :items="categories"
        v-model="selectedCategory"
        @update:model-value="onCategoryChange"
      ></v-select>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  name: 'ProductFilter',
  props: {
    categories: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      selectedCategory: 'all', // Default category
    };
  },
  methods: {
    onCategoryChange(value) {
      this.selectedCategory = value;
      this.emitFilterChange();
    },
    emitFilterChange() {
      console.log('Category filter changed:', this.selectedCategory);
      this.$emit('filter-changed', {
        category: this.selectedCategory,
      });
    },
  },
};
</script>
