<template>
  <div class="quote-container" id="quote-container">
    <!-- quote -->
    <div class="quote-text" v-if="apiQuotes">
      <img
        alt="Vue logo"
        class="quote-icon"
        src="@/assets/left-quote-sketch-svgrepo-com.svg"
      />
      <span id="quote"> {{ myQuote.text }}</span>
      <!-- Author -->
      <div class="quote-author">
        <span id="author" v-if="myQuote.author">-{{ myQuote.author }}</span>
        <span class="" v-else>-Unkown</span>
      </div>
      <!-- Button -->
      <div class="button-container">
        <img
          alt="twitter icon"
          class="twitter-icon center-inter"
          src="@/assets/twitter-icon.svg"
        />
        <button class="twitter center-inter" id="twitter" title="Tweet This">
          <a class="link" :href="tweetLink" target="_blank">
            Share this on twitter
          </a>
        </button>
      </div>
    </div>
  </div>
</template>

<style>
a:link {
  text-decoration: none;
  font-family: "Roboto", sans-serif;
}

.quote-container {
  width: auto;
  max-width: 900px;
  padding: 1rem 1.5rem;
  border-radius: 10px;
  background-color: rgba(255, 255, 255, 0.4);
  box-shadow: 0 0.2rem 0.2rem 0.2rem rgba(0, 0, 0, 0.4);
}
.quote-text {
  font-size: 2.7rem;
  font-family: "Roboto", sans-serif;
}
.quote-author {
  margin-top: 1vh;
  font-size: 2rem;
  font-weight: 400;
  font-style: italic;
}
.long-quote {
  font-size: 2rem;
}
.quote-icon {
  padding: 5px 5px;
  width: 3rem;
  height: auto;
}
.twitter-icon {
  width: 2rem;
  height: auto;
}
.link {
  color: #fff;
  font-style: normal;
}
.button-container {
  margin-top: 15px;
  display: flex;
  justify-content: center;
}
.center-inter {
  padding: 0 1rem;
}
button {
  cursor: pointer;
  font-size: 1.2rem;
  height: 2.5rem;
  border: none;
  border-radius: 10px;
  color: #fff;
  background-color: #333;
  outline: none;
  padding: 0.5rem 1.8rem;
}
button:hover {
  filter: brightness(110%);
}
button:active {
  transform: translate(0 0.3rem);
}
</style>
<script>
// import axios from "axios";

export default {
  data() {
    return {
      apiQuotes: [],
    };
  },
  methods: {
    getQuotes() {
      const apiUrl = "https://type.fit/api/quotes";

      fetch(apiUrl)
        .then((response) => {
          return response.json();
        })
        .then((data) => (this.apiQuotes = data))
        .catch("Failed to grab quotes");
    },
    getSingleQuote() {
      this.apiQuotes[Math.floor(Math.random() * this.apiQuotes.length - 1)];
    },
  },
  computed: {
    myQuote() {
      return this.apiQuotes[
        Math.floor(Math.random() * this.apiQuotes.length - 1)
      ];
    },
    tweetLink() {
      return `https://twitter.com/intent/tweet?text=${this.myQuote.text} - ${this.myQuote.author}`;
    },
  },
  created() {
    this.getQuotes();
  },
  mounted() {},
};
</script>
