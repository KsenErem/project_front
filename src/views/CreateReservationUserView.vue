<template>
  <div class="horizonatal">
    <div class="navigation-menu">
      <button class="start-button" @click="$router.push('/profileUser')">← На главную</button>
      <button class="center-button color"  >Создание брони</button>
    </div>
    <div class="content">
      <div class="reservation-box">


        <div class="user-box">
          <div class="column">
            <span v-html="name"></span>
            <span v-html="phone"></span>
          </div>
          <div class="column horizontal">
            <div class="selection-previous" @click="decrementDate"><</div>
            <div class="date-picker"><label v-html="reservationPeriod.date"></label></div>
            <div class="selection-next" @click="incrementDate">></div>
            <div class="spacer">-</div>
            <div class="time-selector">
              <masked-input v-model="reservationPeriod.startTime" mask="11:11" placeholder="00:00" />
              <label>-</label>
              <masked-input v-model="reservationPeriod.endTime" mask="11:11" placeholder="00:00" />
            </div>

          </div>
        </div>
        <button class="create-reservation-button color" @click="createReservation">Создать бронь</button>
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";
import Vue from "vue";
import MaskedInput from 'vue-masked-input';
import axios from "axios";

export default {
  name: "CreateReservationUserView",
  data() {
    return {
      offsetDays: 0,
      name: '',
      phone: '',
      gender: " ",
      id: '',
      reservationPeriod: {
        date: moment().format("YYYY-MM-DD"),
        startTime: '',
        endTime: ''
      },
      selectedGender: 0
    }
  },
  components:{
    MaskedInput
  },
  mounted() {
    this.Test();
  },
  methods: {
    Test() {
      console.log(window.apiUrl);
      let token = localStorage.getItem("jwt_token");
      const config = {
        headers: { Authorization: `Bearer ${token}` },
      };

      axios.post(`${window.apiUrl}/auth/checkToken`, {}, config).then(response => {
        // Token is valid, so continue
        console.log(response)
        this.name = response.data.data.user.name
        this.phone = response.data.data.user.login
        this.gender = response.data.data.user.gender
        console.log(this.name)
      }).catch(error => {
        // There was an error so redirect
        console.log("Обидно")
      })

    },

    decrementDate: function () {
      this.offsetDays++;
      this.reservationPeriod.date = moment(Date.now()).subtract(this.offsetDays, 'days').format("YYYY-MM-DD");
    },
    incrementDate: function () {
      this.offsetDays--;
      this.reservationPeriod.date = moment(Date.now()).subtract(this.offsetDays, 'days').format("YYYY-MM-DD")
    },
    createReservation: async function(){
      if(!this.name || !this.phone || !this.reservationPeriod.startTime || !this.reservationPeriod.endTime){
        this.$toast.error('Заполните все поля клиента', 'Ошибка');
        return;
      }

      if(this.reservationPeriod.startTime.split(':')[1] !== '00' && this.reservationPeriod.startTime.split(':')[1] !== '30'){
        this.$toast.error('Минуты брони могут быть только :00 либо :30', 'Ошибка');
        return;
      }

      if(this.reservationPeriod.endTime.split(':')[1] !== '00' && this.reservationPeriod.endTime.split(':')[1] !== '30'){
        this.$toast.error('Минуты брони могут быть только :00 либо :30', 'Ошибка');
        return;
      }
      // 2022-07-03 17:30:00
      let startDate = moment(Date.now()).subtract(this.offsetDays, 'days').format("YYYY-MM-DD");
      let endDate = moment(Date.now()).subtract(this.offsetDays, 'days').format("YYYY-MM-DD");
      if(this.reservationPeriod.endTime.split(':')[0] < this.reservationPeriod.startTime.split(':')[0]){
        console.log(`another day`);
        endDate = moment(Date.now()).subtract(this.offsetDays - 1, 'days').format("YYYY-MM-DD")
      }

      let startTime = `${startDate} ${this.reservationPeriod.startTime}:00`;
      let endTime = `${endDate} ${this.reservationPeriod.endTime}:00`;


      try {
        let result = await Vue.axios({
          method: 'post',
          url: `${window.apiUrl}/reservations/create`,
          data: {
            start_time: startTime,
            end_time: endTime,
            gender: this.gender,
            name: this.name,
            phone: this.phone,
          },
          headers: {
            "Authorization": `Bearer ${localStorage.getItem("jwt_token")}`
          }
        });
        let data = result.data.data;
        console.log(data);

        if(result.status === 200){
          this.$toast.success("Добавлено", "Получилось!", {position: "bottomCenter"});
        }
      }
      catch(error){
        this.$toast.error(error.response.data.message, 'Ошибка')
      }
    }
  }
}
</script>

<style scoped>

</style>