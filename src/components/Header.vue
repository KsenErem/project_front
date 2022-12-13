<template>
    <div class="header">
      <header class="d-flex flex-wrap justify-content-center py-3 mb-4 border-bottom">
        <a href="/" class="d-flex align-items-center mb-3 mb-md-0 me-md-auto text-dark text-decoration-none">
          <a class="navbar-brand logo" href="/">AVS Кристалл</a>
        </a>


        <ul class="nav col-12 col-md-auto mb-2 justify-content-center mb-md-0">
          <li><a href="/about" class="nav-link px-2 link-dark">О нас</a></li>
          <li><a href="/contacts" class="nav-link px-2 link-dark">Контакты</a></li>
        </ul>

        <div class="col-md-3 text-end">
          <a v-if="authStatus && resWhere" href="/login" type="button" class="btn btn-outline-primary me-2" >Выход</a>
          <a v-else-if="authStatus && gender === (0 || 1)" href="/profileUser" type="button" class="btn btn-outline-primary me-2" >Профиль</a>
          <a v-else-if="authStatus && gender === 2" href="/homeAdmin" type="button" class="btn btn-outline-primary me-2" >Профиль</a>
          <a v-else href="/login" type="button" class="btn btn-outline-primary me-2" >Вход</a>
        </div>
      </header>
    </div>


</template>




<script>
import axios from "axios";
import Vue from "vue";

export default {
  name: "Header",
  props: {
    msg: String
  },
  data: function(){
      return { authStatus: false, gender: -1, resWhere: false}
    },
  mounted() {
    this.Test()
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
          this.gender = response.data.data.user.gender
        }).catch(error => {
          // There was an error so redirect
          this.authStatus = false
        })
      console.log(window.location.pathname === '/homeAdmin')
      if (window.location.pathname === '/homeAdmin' || window.location.pathname === '/profileUser') {
        this.resWhere = true;
      }
    }
  }
}
</script>

<style >
.header{
  background-color: #F0F8FF;
  background-size: 100% auto;
}
.logo{
  padding-right: 180px;
}

</style>