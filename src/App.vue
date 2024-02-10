<script>
import axios from "axios";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import Card from "./components/Card.vue";
import Title from "./components/Title.vue";
import Button from "./components/Button.vue";

export default {
  name: "App",
  components: {
    Header,
    Card,
    Footer,
    Title,
    Button,
  },
  data() {
    return {
      appName: "Yu-Gi-Oh API",
      footerText: "Marco Finucci, Boolean Course",
      fetchBaseURL: "https://db.ygoprodeck.com/api/v7/cardinfo.php",
      isLoading: true,
      isError: false,
      cards: [],
      cardsPerPage: 15,
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
  <Header :appName="appName" />

  <!-- Main -->
  <main class="py-12">
    <div class="container">
      <!-- If loading -->
      <div v-if="isLoading">
        <Title text="Loading..." />
      </div>

      <!-- If error -->
      <div v-else-if="isError">
        <Title text="Error loading data" />
      </div>

      <!-- If loaded -->
      <div v-else>
        <!-- Cards number -->
        <Title :text="'Showed ' + cardsShowed + ' cards'" />

        <!-- Cards list -->
        <div class="mt-8 grid gap-8 sm:grid-cols-2 md:grid-cols-3 xl:grid-cols-5">
          <div v-for="card in cards">
            <Card :card="card" />
          </div>
        </div>

        <!-- Load more button -->
        <Button @click-button="loadMoreCards" text="Load more cards" />
      </div>
    </div>
  </main>

  <!-- Footer -->
  <Footer :text="'Showed ' + cardsShowed + ' cards | ' + footerText" />
</template>
