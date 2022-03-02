<template>
  <div class="card mb-3">
    <div class="row g-0">
      <div class="col-md-4">
        <div class="row g-0">
          <img
            style="margin: 10px"
            src="../assets/sun.png"
            class="img-fluid rounded-start"
            v-if="weather.weather[0].main == 'Clear'"
          />
          <img
            style="margin: 10px"
            src="../assets/rain.png"
            class="img-fluid rounded-start"
            v-else-if="weather.weather[0].main == 'Rain'"
          />
          <img
            style="margin: 10px"
            src="../../public/snow.png"
            class="img-fluid rounded-start"
            v-else-if="weather.weather[0].main == 'Snow'"
          />
          <img
            style="margin: 10px"
            src="../assets/clouds.png"
            class="img-fluid rounded-start"
            v-else-if="weather.weather[0].main == 'Clouds'"
          />
          <img
            style="margin: 10px"
            src="../assets/weather-alert.png"
            class="img-fluid rounded-start"
            v-else
          />
        </div>
        <div class="row g-0" style="text-align: center">
          <h2 style="margin-left: 15px">
            {{ Math.round(weather.main.temp) }}<span>&deg;</span> C
          </h2>
        </div>
      </div>
      <div class="col-md-8">
        <div class="card-body" style="margin-top: 90px">
          <h5 class="card-title">
            {{ weather.name }}, {{ weather.sys.country }}
          </h5>
          <p class="card-text">
            <b>{{ weather.weather[0].main }}</b>
          </p>
          <p class="card-text">
            <small class="text-muted">{{ dateBuilder() }}</small>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Content",
  props: {
    weather: Object,
  },
  methods: {
    dateBuilder() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return day + " " + date + " " + month + " " + year;
    },
  },
};
</script>

<style scoped>
p,
h5 {
  color: #868383;
  font-size: 24px;
}

h2 {
  font-size: 32px;
  line-height: 50px;
  font-weight: 900;
  color: #868383;
}

.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.7);
  transition: 0.3s;
  border-radius: 16px;
  background-color: rgba(255, 255, 255, 0.6);
  backdrop-filter: blur(24px);
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.7);
  background-color: rgba(255, 255, 255, 0.9);
}
</style>
