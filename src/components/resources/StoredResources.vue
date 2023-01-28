<template>
  <ul>
    <learning-resource v-for="resource of resources"
                       :key="resource.id"
                       :id="resource.id"
                       :title="resource.title"
                       :description="resource.description"
                       :link="resource.link">
    </learning-resource>
  </ul>
</template>

<script>
import LearningResource from '@/components/resources/LearningResource.vue';

export default {
  name: 'StoredResources',
  components: { LearningResource },
  inject: ['resources']
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0 auto;
  padding: 0;
  max-width: 40rem;
}
</style>
