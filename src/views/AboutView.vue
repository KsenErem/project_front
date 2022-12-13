<template>
  <div class="about">
      <Header />
    <div class="container marketing">
      <div class="row featurette">
        <div class="col-md-7 object_center_middle">
          <hr class="featurette-divider color-link">
          <h2 class="featurette-heading fw-normal lh-1 headline">О нас</h2>
          <hr class="featurette-divider color-link">
          <p class="lead color-text">
            Спортивно-оздоровительный центр “AVS Кристалл” подойдет для проведения мероприятий и соревнований любого типа.
            Тут есть все условия для любителей спорта и тех, кто просто старается поддерживать форму и вести здоровый образ жизни.
          </p>
        </div>
        <div class="col-md-5">
          <img class="bd-placeholder-img bd-placeholder-img-lg featurette-image img-fluid mx-auto img"
               src="../assets/images/hDpXllA6xDo.jpg" ></img>
        </div>
      </div>
      <hr class="featurette-divider color-link">
        <h4 class="headline"> Партнёры</h4>
      <hr class="featurette-divider color-link">
        <div class="row ">
          <div class="col-lg-3 rectangle">
            <div class="object_center_middle">
              <span class="circle-image">
             <img src="https://www.usue.ru/public/files/loaded/5d0cb63cb9ebd.jpg"/>
            </span>
              <h2 class="fw-normal"><a class="color-text" target="_blank" href="https://ekburg.tv/">АиФ Урал</a></h2>
              <p class="color-text">Новости спорта в Екатеринбурге</p>
            </div>
          </div><!--/.col-lg-4 -->
          <div class="col-lg-3 rectangle">
            <div class="object_center_middle">
              <span class="circle-image">
             <img src="https://www.toptj.com/images/news/2022-08-03-02.jpg"/>
            </span>
              <h2 class="fw-normal"><a class="color-text" target="_blank" href="https://legalbet.ru/tips/today/">Legalbet</a></h2>
              <p class="color-text">Прогнозы на спорт</p>
            </div>
          </div><!-- /.col-lg-4 -->
          <div class="col-lg-3 rectangle">
            <div class="object_center_middle">
              <span class="circle-image">
             <img src="https://www.komuza.net/wp-content/uploads/2018/05/ЕТВ_new-3.png"/>
            </span>
              <h2 class="fw-normal"><a class="color-text" target="_blank" href="https://ekburg.tv/">ЕТВ</a></h2>
              <p class="color-text">Новости и трансляции событий в ЕКБ</p>
            </div>
          </div><!-- /.col-lg-4 -->
        </div><!-- /.row -->
      <hr class="featurette-divider color-link">

    </div>
    <Footer />
    </div>

</template>

<script>
import Header from '@/components/Header.vue'
import MainContainer from '../components/MainContainer'
import Footer from "@/components/Footer";
export default {
  name: 'AboutView',
  components: {
    Header,
    Footer,
    MainContainer,
  },
  data() {
    return {
      login: '',
      password: '',
    }
  },
  methods: {
  },

}
</script>

<style>
.body {
  background: url("../assets/images/hDpXllA6xDo.jpg");
  color: #000000; /*Цвет текста на странице*/
  background-attachment: fixed; /* Фон страницы фиксируется */
  background-repeat: repeat-x; /* Изображение повторяется по горизонтали */
  background-size: 100%;
}
.about{
  background-size: 100%;
}
.color-text{
  color: black;
}
.circle-image{
  display: inline-block;
  border-radius: 50%;
  overflow: hidden;
  width: 140px;
  height: 140px;
}
.circle-image img{
  width:100%;
  height:100%;
  object-fit: cover;
}
.color-link{
  background-color: #BDE0FF;
}
.rectangle {
  width: 100px;
  height: 300px;
  background: white;
  margin-right: 40px;
  margin-left: 40px;
}
.object_center_middle{
  margin-left: auto;
  margin-right: auto;
  margin-top: 10%;
  vertical-align: middle
}
.img{
  width: 500px ;
  height: 500px
}
.headline{
  color: #00006f;
}
</style>