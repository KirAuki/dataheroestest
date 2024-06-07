<template>
    <div class="pagination">
      <button @click="prevPage" :disabled="!info.prev">Previous</button>
      <span>Page {{ currentPage }} of {{ info.pages }}</span>
      <button @click="nextPage" :disabled="!info.next">Next</button>
    </div>
</template>
  
<script>
  export default {
    name: 'Pagination',
    props: {
      info: Object,
      currentPage: Number,
    },
    emits: ['page-change'],
    methods: {
      prevPage() {
        if (this.info.prev) {
          this.$emit('page-change', this.currentPage - 1);
        }
      },
      nextPage() {
        if (this.info.next) {
          this.$emit('page-change', this.currentPage + 1);
        }
      },
    },
  };
</script>
  
<style scoped>
  .pagination {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
  }
</style>
  