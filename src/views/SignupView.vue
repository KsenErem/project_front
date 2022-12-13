<template>
  <section class="vh-100 gradient-custom">
    <div class="container py-5 h-100">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col-12 col-md-8 col-lg-6 col-xl-5">
          <div class="card bg-dark text-white" style="border-radius: 1rem;">
            <div class="card-body p-5 text-center">

              <div class="mb-md-5 mt-md-4 pb-5">

                <h2 class="fw-bold mb-2 text-uppercase">Регистрация</h2>
                <p class="text-white-50 mb-5">Введите свои данные</p>

                <div class="form-outline form-white mb-4">
                  <input v-model="name" type="text" id="typeNameX" class="form-control form-control-lg"/>
                  <label class="form-label" for="typeNameX">Имя</label>
                </div>

                <div class="form-outline form-white mb-4">
                  <input v-model="login" type="number" id="typeNumberX" class="form-control form-control-lg"/>
                  <label class="form-label" for="typeNumberX">Номер телефона</label>
                </div>

                <div class="form-outline form-white mb-4">
                  <input type="password" v-model="password" id="typePasswordX" class="form-control form-control-lg"/>
                  <label class="form-label" for="typePasswordX">Пароль</label>
                </div>

                <div class="form-outline form-white mb-4">
                  <input type="password" v-model="repeatpassword" id="typeRepeatPasswordX" class="form-control form-control-lg"/>
                  <label class="form-label" for="typeRepeatPasswordX">Повторите пароль</label>
                </div>

                <div class="form-outline form-white mb-4" id="pol">
                  <div class="row ">
                    <div class="col-lg-6 button">
                      <span class="btn btn-lg px-5" @click="setM(0)"><span :class="gender0">Женский</span></span>
                    </div>
                    <div class=" col-lg-6 button">
                      <span class="btn btn-lg px-5" @click="setM(1)"><span :class="gender1">Мужской</span></span>
                    </div>
                  </div>
                  <label class="form-label" for="pol">Пол</label>
                </div>



                <button class="btn btn-outline-light btn-lg px-5" @click="RegUser">Регистрация</button>

                <div class="form-outline mb-6 px-5 ">
                  <label class="form-label mb-6">У вас уже есть аккаунт?</label>
                  <a href="/login" type="button" class="btn btn-outline-light btn-lg px-5">Вход</a>
                </div>


              </div>

            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Vue from "vue";

export default {
  name: "SignupView",
  components: {},
  data() {
    return {
      name: '',
      login: '',
      password: '',
      repeatpassword: '',
      gender: '',
      toasts: {
        error: {
          position: "topRight"
        }
      },
    }
  },
  computed: {
    gender1: function() {
      if(this.gender === 1) {
        return 'green'
      } else {
        return 'red'
      }
    },
    gender0: function() {
      if(this.gender === 0) {
        return 'green'
      } else {
        return 'red'
      }
    }
  },
  methods: {
    setM: function(p) {
      this.gender = p;
      console.log(this.gender)
    },
    async RegUser(event) {
      try {
        console.log(this.login, this.password);

        if (!this.login || !this.password || !this.repeatpassword || !this.name || this.gender === '' ) {
          Vue.toast('<label>Введите данные</label>');
          return;
        }

        if (this.password !== this.repeatpassword ) {
          Vue.toast('<label>Пароли не совпадают</label>');
          return;
        }

        let result = await Vue.axios({
          method: 'post',
          url: `${window.apiUrl}/auth/register`,
          data: {
            name: this.name,
            login: this.login,
            password: this.password,
            gender: this.gender,
          }
        });
        let data = result.data.data;
        console.log(result);
        if (result.status === 200) {
          console.log(`here`);
          localStorage.setItem("jwt_token", data.token);
          window.location.href = "/profileUser";
        }
        console.log(localStorage.getItem("jwt_token"));
      }catch (e) {
        this.$toast.error('Данные не верны', 'Error')
      }
    }
    },
}
</script>

<style>
.red {
  color: white;
}

.green {
  color: white;
  text-decoration: underline;
}

</style>