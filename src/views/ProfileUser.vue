<template>
  <div class="profile">
    <Header />

    <div class="container mt-5 d-flex justify-content-center">
      <div class="card p-3">
        <div class="d-flex align-items-center">
          <div class="image">
            <img src="https://images.unsplash.com/photo-1522075469751-3a6694fb2f61?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=500&q=80" class="rounded" width="155" >
          </div>
          <div class="ml-3 w-100">
            <h4 class="mb-0 mt-0"><span v-html="name"></span></h4>
            <div class="button mt-2 d-flex flex-row align-items-center">
              <p>Телефон: <span v-html="number"></span></p>
            </div>
            <div class="button mt-2 d-flex flex-row align-items-center">
              <p>Запись: </p><p>Время и дата записи</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="horizonatal">
      <div class="navigation-end-menu">
        <button class="end-button color" @click="$router.push('/createReservationUser')">Создать бронь</button>
      </div>
      <div class="selector" style="display: flex; justify-content: center; margin-top: 20px">
        <div class="selection-previous" @click="decrementDate"><</div>
        <div class="date-picker color" :class="{today: this.offsetDays == 0}"><label v-html="selectedDate"> </label></div>
        <div class="selection-next" @click="incrementDate">></div>
      </div>

      <div class="table-wrapper">

        <table>

          <tr>

          </tr>

        </table>
      </div>
    </div>
    <Footer />
  </div>



</template>

<script>
import Header from '@/components/Header.vue'
import VCalendar from 'v-calendar';
// Import Vue
import Vue from 'vue';

// Import VueScheduler
import VueScheduler from 'v-calendar-scheduler';
import Footer from "@/components/Footer";
import axios from "axios";
import moment from "moment/moment";
import Modal from "@/components/Modal";

// Import styles


Vue.use(VueScheduler);
export default {
  name: "ProfileUser",
  components: {
    Header,
    Footer
  },
  props: {
    msg: String
  },
  data: function(){
    return {
      name: "",
      number: "",
      gender: " ",
      login: '',
      password: '',
      selectedDate: moment().format("YYYY-MM-DD"),
      offsetDays: 0,
    }
  },
  mounted() {
    console.log(`vue is `, Vue.$api);
    this.Test();
    this.createTable();
  },
  methods:{
    Test() {
      console.log(window.apiUrl);
      let token = localStorage.getItem("jwt_token");
      const config = {
        headers: { Authorization: `Bearer ${token}` },
      };

      axios.post(`${window.apiUrl}/auth/checkToken`, {}, config).then(response => {
        // Token is valid, so continue
        this.authStatus = true;
        console.log(response)
        this.name = response.data.data.user.name
        this.number = response.data.data.user.login
        this.gender = response.data.data.user.gender
        console.log(this.name)
      }).catch(error => {
        // There was an error so redirect
        this.authStatus = false
      })

    },
    decrementDate: function () {
      this.offsetDays++;
      this.selectedDate = moment(Date.now()).subtract(this.offsetDays, 'days').format("YYYY-MM-DD");
      this.createTable();
    },
    incrementDate: function () {
      this.offsetDays--;
      this.selectedDate = moment(Date.now()).subtract(this.offsetDays, 'days').format("YYYY-MM-DD");
      this.createTable();
    },

    createTable: async function () {
      let gender = this.gender;
      try {
        let result = await Vue.axios({
          method: 'get',
          url: `${window.apiUrl}/reservations/getTable?gender=${gender}`,
          headers: {
            "Authorization": `Bearer ${localStorage.getItem("jwt_token")}`
          }
        });

        let data = result.data.data;

        let table = document.querySelector("table");
        let firstRow = document.createElement("tr");

        this.removeAllChildNodes(table);

        for (let i = 0; i < data.columns.length; i++) {
          let currentTime = data.columns[i];
          let tableHeader = document.createElement("th");
          tableHeader.setAttribute('data-time', currentTime);
          tableHeader.innerText = currentTime;
          tableHeader.style.backgroundColor = "#BDE0FF";
          tableHeader.style.fontFamily = "Montserrat";
          tableHeader.style.fontWeight = "800";
          firstRow.append(tableHeader);
        }

        table.append(firstRow);


        for (let i = 0; i < data.rows; i++) {
          let newRow = document.createElement("tr");
          for (let k = 0; k < data.columns.length; k++) {

            let currentTime = data.columns[k];
            let cell = document.createElement("td");
            cell.setAttribute('data-time', currentTime);
            newRow.append(cell);
          }
          table.append(newRow);
        }



        result = await Vue.axios({
          method: 'get',
          url: `${window.apiUrl}/reservations/?start_time=${this.selectedDate} 08:00:00&end_time=${moment(Date.now()).subtract(this.offsetDays - 1, 'days').format("YYYY-MM-DD")} 03:00:00&gender=${this.gender}"`,
          headers: {
            "Authorization": `Bearer ${localStorage.getItem("jwt_token")}`
          },
        });
        console.log(`response`, result.data.data);

        var width = document.querySelector('td').getBoundingClientRect().width;

        let rowCounter = 1;


        for (let res = 0; res < result.data.data.length; res++) {
          let currentRow = document.querySelectorAll("table tr")[rowCounter];

          let reservation = result.data.data[res];

          console.log(reservation);

          let startTime = moment(reservation.start_time).local(true);
          console.log(startTime);
          let endTime = moment(reservation.end_time).local(true);
          let duration = endTime.diff(startTime, 'minutes');

          let cellWidth = (duration / 30);
          let pixelWidth = ((duration / 30)) * width;

          let startCell = `${startTime.get('hours') || '00'}:${startTime.get('minutes') || '00'}`;
          let targetCell = currentRow.querySelector(`td[data-time="${startCell}"]`);
          let index = [...currentRow.children].indexOf(targetCell);

          let neededDropOut = false;
          for (let k = index; k < index + cellWidth; k++) {
            if (currentRow.children[k].getAttribute('data-used')) {
              neededDropOut = true;
            }
          }

          if (neededDropOut == true) {
            rowCounter++;
            res--;
            continue;
          }

          console.log(`res`, reservation.status);

          let scheduleCell = document.createElement("a");
          scheduleCell.style.position = "absolute";
          scheduleCell.style.top = "1px";
          scheduleCell.style.left = "2px";
          scheduleCell.setAttribute('href', '#');
          scheduleCell.style.width = `${pixelWidth - 4}px`;
          scheduleCell.style.height = "22px";
          scheduleCell.style.backgroundColor = "#E0E0E0";
          scheduleCell.style.color = "white";
          if(reservation.status === '1'){
            scheduleCell.style.backgroundColor = "#E0E0E0";
            scheduleCell.style.color = "#000000";
          }
          scheduleCell.style.textAlign = "left";
          scheduleCell.style.fontFamily = "Montserrat";
          scheduleCell.style.fontWeight = "600";
          scheduleCell.innerText = reservation.client_name;
          scheduleCell.style.zIndex = "5";
          scheduleCell.style.color = "#000000"
          scheduleCell.style.textDecoration = "none";

          scheduleCell.style.textIndent = "5px";
          scheduleCell.style.overflow = "hidden";
          scheduleCell.style.textOverflow = "ellipsis";
          scheduleCell.setAttribute('data-id', reservation.id);

          scheduleCell.addEventListener("click", async (event) => {
            let id = event.target.getAttribute('data-id');

            result = await Vue.axios({
              method: 'get',
              url: `${window.apiUrl}/reservations/getSingle?id=${id}`,
              headers: {
                "Authorization": `Bearer ${localStorage.getItem("jwt_token")}`
              },
            }).catch(error => {
              console.log(`error here`, error);
            });

            let data = result.data.data;

          })


          targetCell.append(scheduleCell);



          for (let k = index; k < index + cellWidth; k++) {
            currentRow.children[k].setAttribute('data-used', 'true');
          }


          rowCounter = 1;
        }

      } catch (error) {
        console.log(`error`, error);
        if (error.response.status === 403) {
          window.location.href = '/login';
        }
      }
    },
    removeAllChildNodes: function (parent) {
      while (parent.firstChild) {
        parent.removeChild(parent.firstChild);
      }
    },

  }

}

</script>

<style>
@import 'v-calendar-scheduler/lib/main.css';
body{
  border-radius: 10px;

}

.profile{
  background-size: 100%;
}

.card{
  width: 500px;
  border: none;
  border-radius: 10px;

  background-color: #BDE0FF;
}



.stats{

  background: #000000 !important;

  color: #000 !important;
}
.articles{
  font-size:10px;
  color: #a1aab9;
}
.number1{
  font-weight:500;
}
.followers{
  font-size:10px;
  color: #a1aab9;

}
.number2{
  font-weight:500;
}
.rating{
  font-size:10px;
  color: #a1aab9;
}
.number3{
  font-weight:500;
}



</style>