<template>
  <div class="horizonatal">
    <div class="navigation-menu">
      <button class="start-button" @click="$router.push('/homeAdmin')">← На главную</button>
      <button class="center-button color"  >Создание брони</button>
    </div>
    <div class="content">
      <Reservation ID="1"></Reservation>
      <Reservation ID="2"></Reservation>
    </div>
  </div>
</template>

<script>

import '../css/index.css';

import Reservation from "../components/Reservation";
import axios from "axios";

export default {
  name: 'CreateReservation',
  components: { Reservation },
  methods: {},

}
</script>

<style>
.color{
  background-color: #BDE0FF;
}
</style>
