<template>
  <div class="box-content-pronostic">
    <div class="box-pronostic" v-for="item in forecast" :key="item.id">
      <p class="box-pronostic-time">
         Day: {{item.time.slice(8,10)}}
          <br>{{item.time.slice(11,13) * 1}}:00
      </p>
    <img :src="require(`@/assets/img/${item.icon}.png`)" />
      <span class="box-pronostic-temperature">{{Math.round(item.temperature)}}°</span>
    </div>
  </div>
</template>
<script>
import "./style.css"
export default {
  props: ["forecast"],
};
</script>

