<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <DataBoxes :stats="stats" />
  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching data</div>
    <img class="w-10 m-auto" :src="loadingImg" alt="" />
  </main>
</template>

<script>
import DataBoxes from "../components/DataBoxes.vue";
import DataTitle from "../components/DataTitle.vue";

export default {
  name: "home",
  components: { DataTitle, DataBoxes },
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      stats: "",
      countries: [],
      loadingImg: require("../assets/hourglass.gif"),
    };
  },
  methods: {
    async fetchCovidData() {
      const rez = await await fetch("https://api.covid19api.com/summary");
      const data = await rez.json();
      return data;
    },
  },
  async created() {
    const data = await this.fetchCovidData();
    this.dataDate = data.Date;
    this.countris = data.Countries;
    this.stats = data.gloabal;

    this.loading = false;

    console.log(data);
  },
};
</script>
