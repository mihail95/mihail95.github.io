<template>
  <div class="publication" v-on:click="visitProject()">
    <div class="title">
      {{ pubTitle }}
    </div>
  </div>
</template>

<script setup>
import { languageStore } from '@/stores/language.js'
import { ref, watch } from 'vue';

const store = languageStore()
const selectedLang = ref(store.language);

watch(
  () => store.language,
  (newLang) => {
    selectedLang.value = newLang;
  }
);
</script>

<script>
export default {
  name: "PublicationComponent",
  props: {
    presentation: Object
  },

  data() {
    return {
      pubTitle: this.presentation.title,
      file_name: this.presentation.file_name,
    };
  },
  methods: {
    visitProject() {
      window.open(`/presentations/${this.file_name}`, '_blank')
    }
  },
};
</script>

<style scoped>
.publication {
  display: flex;
  flex-direction: column;
  width: 95%;
  flex-wrap: nowrap;
  text-wrap: wrap;
  background-color: #222;
  border-radius: 1em;
  padding: 1em;
  margin-bottom: 1.5rem;
  transition: background-color 0.25s ease;
}

.publication:hover {
  cursor: pointer;
  background-color: #3c3c3c;
}

.title {
  color: #66B95C;
  font-weight: 700;
  font-size: 1.25rem;
  flex-grow: 0;
  flex-shrink: 0;
  flex-basis: max-content;
  border-bottom: 1px dashed rgba(255, 255, 255, 0.15);
}
</style>