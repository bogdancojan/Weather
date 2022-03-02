<template>
  <div class="container container-main">
    <input
      type="text"
      placeholder="Search..."
      v-model="query"
      @keypress="fetchWeather"
    />
    <Content :weather="weather" v-if="typeof weather.main != 'undefined'" />
  </div>
</template>

<script>
import Content from "./views/Content.vue";

export default {
  name: "App",
  components: {
    Content,
  },
  data() {
    return {
      api_key: "96aa65a040e7ffb4327afcf6c0ecaa55",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    async fetchWeather(e) {
      if (e.key == "Enter") {
        const res = await fetch(
          this.url_base +
            "weather?q=" +
            this.query +
            "&units=metric&APPID=" +
            this.api_key
        );

        this.weather = await res.json();
        this.query = "";
      }
    },
  },
};
</script>

<style>
#app {
  font-family: "Times New Roman", Times, serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: auto;
  width: 50%;
}

.container-main {
  margin-top: 60px;
  height: 80vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
}

input {
  width: 40%;
  padding: 12px 20px;
  margin: 8px 0;
  border-radius: 16px;
  border: none;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
}

input:focus {
  outline: none;
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}
</style>
