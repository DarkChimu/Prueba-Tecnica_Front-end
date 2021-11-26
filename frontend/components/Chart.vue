<template>
 <div>
   <h2>
     Seguidores
   </h2>
    <GChart
      type="PieChart"
      :options="options"
      :data="datas"
    /> 
  </div>
</template>

<script>
import { GChart } from "vue-google-charts"

export default {
  name: "Chart",
  components: {
    GChart
  },
  data() {
    return {
      options: {
        width: 500,
        height: 400,
      }
    }
  },
  props: {
    datas: {
      type: Array,
      required: false,
      default: () => [],
    },
  },
};
</script>