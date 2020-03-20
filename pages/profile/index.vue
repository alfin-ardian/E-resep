<template>
  <div>
    <card />
    <pagination />
  </div>
</template>
<script>
import search from "~/components/search.vue";
import card from "~/components/card.vue";
import pagination from "~/components/pagination.vue";
export default {
  components: {
    search,
    card,
    pagination
  }
};
</script>
