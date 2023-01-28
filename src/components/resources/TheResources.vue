<template>
  <base-card>
    <base-button @click="selectTab('stored-resources')" :mode="storedButtonMode">Stored Resources</base-button>
    <base-button @click="selectTab('add-resource')" :mode="addButtonMode">Add Resource</base-button>
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from '@/components/resources/StoredResources.vue';
import AddResource from '@/components/resources/AddResource.vue';

export default {
  name: 'TheResources',
  components: { StoredResources, AddResource },
  data() {
    return {
      selectedTab: 'stored-resources',
      resources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation',
          link: 'https://vuejs.org'
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Google to learn...',
          link: 'https://google.com'
        }
      ]
    };
  },
  provide() {
    return {
      resources: this.resources,
      addResource: this.addResource,
      removeResource: this.removeResource
    };
  },
  computed: {
    storedButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    }
  },
  methods: {
    selectTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, link) {
      const resource = {
        id: new Date().toISOString(),
        title,
        description,
        link
      };
      this.resources.unshift(resource);
      this.selectedTab = 'stored-resources';
    },
    removeResource(id) {
      const resourceId = this.resources.findIndex(resource => resource.id === id);
      this.resources.splice(resourceId, 1);
    }
  }
};
</script>

<style scoped>

</style>
