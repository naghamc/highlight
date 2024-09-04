<script>
import { ref } from "vue";

export default {
  setup() {
    const searchTerm = ref("");
    const highlightedText = ref("");
    const occurrences = ref(0);
    const paragraph =
      "this is an example paragraph , you can search for a word in this paragraph";
    const handleSearch = () => {
      highlightedText.value = searchTerm.value;
    };

    const highlightText = (text, term) => {
      occurrences.value = 0;
      if (!term) return text;
      const parts = text.split(new RegExp(`(${term})`, "gi"));
      return parts.map((part) => {
        if (part.toLowerCase() === term.toLowerCase()) {
          occurrences.value += 1;
        }
        return part.toLowerCase() === term.toLowerCase()
          ? `<span style="background-color: yellow;">${part}</span>`
          : part;
      });
    };

    return {
      occurrences,
      searchTerm,
      highlightedText,
      paragraph,
      handleSearch,
      highlightText,
    };
  },
};
</script>

<template>
  <div>
    <p v-html="highlightText(paragraph, highlightedText)"></p>
    <form @submit.prevent="handleSearch">
      <input type="text" v-model="searchTerm" placeholder="Search for a word" />
      <div>{{ occurrences }} of {{ highlightedText }} were found</div>
      <button type="submit">Search</button>
    </form>
  </div>
</template>

<style>
div {
  padding: 20px;
  font-family: Arial, sans-serif;
}

input {
  margin-right: 10px;
  padding: 5px;
}

button {
  padding: 5px 10px;
  cursor: pointer;
}
</style>
