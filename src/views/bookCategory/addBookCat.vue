<template>
  <div>
    <addBookCategory :mode="'addPage'" />
  </div>
</template>


<script>
import addBookCategory from '../../components/bookCategory/addBookCategory.vue';

export default {
  name: 'addBookCat',
  components: {
    addBookCategory,
  },
};
</script>
