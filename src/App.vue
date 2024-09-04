<script>
import { ref } from "vue";

export default {
  setup() {
    const searchTerm = ref("");
    const highlightedText = ref("");
    const paragraph =
      "this is an example paragraph , you can search for a word in this paragraph";
    const handleSearch = () => {
      highlightedText.value = searchTerm.value;
    };

    const highlightText = (text, term) => {
      if (!term) return text;
      const parts = text.split(new RegExp(`(${term})`, "gi"));
      return parts
        .map((part) =>
          part.toLowerCase() === term.toLowerCase()
            ? `<span style="background-color: yellow;">${part}</span>`
            : part
        )
        .join("");
    };

    return {
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
