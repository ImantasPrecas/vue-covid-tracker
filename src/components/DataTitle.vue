<template>
  <div class="text-center">
    <h2 class="text-3xl font-bold">{{ text }}</h2>
    <div class="text-2xl mb-4 mt-10">
      {{ timestamp }}
    </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  name: "DataTitle",
  props: ["text", "dataDate"],
  computed: {
    timestamp: function () {
      return moment(this.dataDate).format("MMMM Do YYYY, kk:mm:ss ");
    },
  },
};
</script>