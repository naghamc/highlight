<template>
  <div class="card-container">
    <h1 style="font-weight: bold">Search</h1>
    <br />
    <form @submit.prevent="handleSearch">
      <input
        type="text"
        v-model="searchTerm"
        placeholder="Search for a word"
        @input="handleSearch"
        size="50"
      />
      <!-- <button type="submit">Search</button> -->
      <br />
      <br />
      <span v-if="highlightedText"
        >{{ occurrences }} of {{ highlightedText }} were found</span
      >
    </form>
    <br />
    <p v-html="highlightText(paragraph, highlightedText)"></p>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const searchTerm = ref("");
    const highlightedText = ref("");
    const occurrences = ref(0);
    const paragraph =
      "Understanding the difference between grid-template and grid-auto Oct 09, 2018 With all the new properties related to CSS Grid Layout, one of the distinctions that always confused me was the difference between the grid-template-* and grid-auto-* properties. Specifically the difference between grid-template-rows/columns and grid-auto-rows/columns. Although I knew they were to d... Recreating the GitHub Contribution Graph with CSS Grid Lavout ";
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

<style>
.card-container {
  background: #f1f1f1; /* White background */
  border-radius: 8px; /* Rounded corners */
  padding: 20px; /* Space inside the card */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Subtle shadow */
  max-width: 600px; /* Maximum width of the card */
  margin: 20px auto; /* Center the card horizontally with some top/bottom margin */
}

input {
  width: calc(100% - 22px); /* Full width minus padding and border */
}
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
