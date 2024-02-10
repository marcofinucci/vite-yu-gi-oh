<script>
import axios from "axios";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import Card from "./components/Card.vue";
import Title from "./components/Title.vue";

export default {
  name: "App",
  components: {
    Header,
    Card,
    Footer,
    Title,
  },
  data() {
    return {
      appName: "Yu-Gi-Oh API",
      footerText: "Boolean Course, powered by Vue",
      fetchBaseURL: "https://db.ygoprodeck.com/api/v7/cardinfo.php",
      isLoading: true,
      isError: false,
      cards: [],
      cardsPerPage: 20,
      cardsShowed: 0,
    };
  },
  mounted() {
    axios
      .get(this.fetchBaseURL + "?num=" + this.cardsPerPage + "&offset=" + this.cardsShowed)
      .then((response) => {
        this.isLoading = false;
        this.cards = response.data.data;
        this.cardsShowed += this.cardsPerPage;
      })
      .catch((error) => {
        this.isLoading = false;
        this.isError = true;
        console.log(error);
      });
  },
  methods: {
    loadMoreCards() {
      axios
        .get(this.fetchBaseURL + "?num=" + this.cardsPerPage + "&offset=" + this.cardsShowed)
        .then((response) => {
          this.isLoading = false;
          this.cards = this.cards.concat(response.data.data);
          this.cardsShowed += this.cardsPerPage;
        })
        .catch((error) => {
          this.isLoading = false;
          this.isError = true;
          console.log(error);
        });
    },
  },
};
</script>

<template>
  <!-- Header -->
  <Header :appName="appName"></Header>

  <!-- Main -->
  <main class="py-12">
    <div class="container">
      <!-- Loading -->
      <div v-if="isLoading">
        <Title title="Loading..."></Title>
      </div>

      <!-- Error -->
      <div v-else-if="isError">
        <Title title="Error loading data"></Title>
      </div>

      <!-- Loaded -->
      <div v-else>
        <!-- Cards number -->
        <Title :title="'Showed ' + cardsShowed + ' cards'"></Title>

        <!-- Cards list -->
        <div class="mt-8 grid gap-8 sm:grid-cols-2 md:grid-cols-3 xl:grid-cols-5">
          <div v-for="card in cards">
            <Card :card="card"></Card>
          </div>
        </div>

        <!-- Load more button -->
        <button class="mx-auto mt-8 table bg-black px-6 py-3 text-white transition-colors hover:bg-gray-800" @click="loadMoreCards()">Load more</button>
      </div>
    </div>
  </main>

  <!-- Footer -->
  <Footer :footerText="'Showed ' + cardsShowed + ' cards - ' + footerText"></Footer>
</template>
