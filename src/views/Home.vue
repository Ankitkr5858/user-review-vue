<template>
  <div>
    <review-cards />
    <review-table />
  </div>
</template>

<script>
import ReviewTable from "@/components/data-tables/ReviewTable.vue";
import ReviewCards from "@/components/widgets/ReviewCards.vue";

export default {
  name: "Home",
  components: {
    ReviewTable,
    ReviewCards,
  },
};
</script>
