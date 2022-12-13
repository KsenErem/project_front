<template>
  <div class="contacts">
      <Header />
    <div class="title"><h1>Контакты</h1></div>
    <div class="center ">
      <div class="row">
        <div class="col-sm-1 icon">
          <svg xmlns="http://www.w3.org/2000/svg" color="#00006f" width="20" height="20" fill="currentColor" class="bi bi-geo-alt" viewBox="0 0 16 16">
            <path d="M12.166 8.94c-.524 1.062-1.234 2.12-1.96 3.07A31.493 31.493 0 0 1 8 14.58a31.481 31.481 0 0 1-2.206-2.57c-.726-.95-1.436-2.008-1.96-3.07C3.304 7.867 3 6.862 3 6a5 5 0 0 1 10 0c0 .862-.305 1.867-.834 2.94zM8 16s6-5.686 6-10A6 6 0 0 0 2 6c0 4.314 6 10 6 10z"/>
            <path d="M8 8a2 2 0 1 1 0-4 2 2 0 0 1 0 4zm0 1a3 3 0 1 0 0-6 3 3 0 0 0 0 6z"/>
          </svg>
        </div>
        <div class="col-sm-4.5 text">
          <address class="blockText"> <b>Адрес:</b> 620010, Екатеринбург, Химмаш, ул. Зои Космодемьянской, 46/Б</address>
        </div>
      </div>
      <div class="row">
        <div class="col-sm-1 icon">
          <svg xmlns="http://www.w3.org/2000/svg" color="#00006f" width="20" height="20" fill="currentColor" class="bi bi-envelope" viewBox="0 0 16 16">
            <path d="M0 4a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v8a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V4Zm2-1a1 1 0 0 0-1 1v.217l7 4.2 7-4.2V4a1 1 0 0 0-1-1H2Zm13 2.383-4.708 2.825L15 11.105V5.383Zm-.034 6.876-5.64-3.471L8 9.583l-1.326-.795-5.64 3.47A1 1 0 0 0 2 13h12a1 1 0 0 0 .966-.741ZM1 11.105l4.708-2.897L1 5.383v5.722Z"/>
          </svg>
        </div>
        <div class="col-sm-2.5 text">
          <p class="blockText"> <b>Почта:</b> mail@avscrystal.ru</p>
        </div>
      </div>
      <div class="row">
        <div class="col-sm-1 icon">
          <svg xmlns="http://www.w3.org/2000/svg" color="#00006f" width="20" height="20" fill="currentColor" class="bi bi-clock" viewBox="0 0 16 16">
            <path d="M8 3.5a.5.5 0 0 0-1 0V9a.5.5 0 0 0 .252.434l3.5 2a.5.5 0 0 0 .496-.868L8 8.71V3.5z"/>
            <path d="M8 16A8 8 0 1 0 8 0a8 8 0 0 0 0 16zm7-8A7 7 0 1 1 1 8a7 7 0 0 1 14 0z"/>
          </svg>
        </div>
        <div class="col-sm-2.5 text">
          <p class="blockText"> <b>График работы:</b> ежедневно с 7:00 до 23:00</p>
        </div>
      </div>
      <div class="row">
        <div class="col-sm-1 icon">
          <svg xmlns="http://www.w3.org/2000/svg" color="#00006f" width="20" height="20" fill="currentColor" class="bi bi-telephone " viewBox="0 0 16 16">
            <path d="M3.654 1.328a.678.678 0 0 0-1.015-.063L1.605 2.3c-.483.484-.661 1.169-.45 1.77a17.568 17.568 0 0 0 4.168 6.608 17.569 17.569 0 0 0 6.608 4.168c.601.211 1.286.033 1.77-.45l1.034-1.034a.678.678 0 0 0-.063-1.015l-2.307-1.794a.678.678 0 0 0-.58-.122l-2.19.547a1.745 1.745 0 0 1-1.657-.459L5.482 8.062a1.745 1.745 0 0 1-.46-1.657l.548-2.19a.678.678 0 0 0-.122-.58L3.654 1.328zM1.884.511a1.745 1.745 0 0 1 2.612.163L6.29 2.98c.329.423.445.974.315 1.494l-.547 2.19a.678.678 0 0 0 .178.643l2.457 2.457a.678.678 0 0 0 .644.178l2.189-.547a1.745 1.745 0 0 1 1.494.315l2.306 1.794c.829.645.905 1.87.163 2.611l-1.034 1.034c-.74.74-1.846 1.065-2.877.702a18.634 18.634 0 0 1-7.01-4.42 18.634 18.634 0 0 1-4.42-7.009c-.362-1.03-.037-2.137.703-2.877L1.885.511z"/>
          </svg>
        </div>
        <div class="col-sm-2.5 text">
          <div class="blockText">
            <div class="col-sm-1.5"><b>Менеджеры:</b> <a href="tel:+73432587197">+7 (343) 258-71-97</a></div>
          </div>

        </div>
      </div>
    </div>

    <iframe src="https://yandex.ru/map-widget/v1/?um=constructor%3A62a379796fae535f08f91f58829ca999f67283f9324091d491ae12437f67b19d&amp;source=constructor"
            width="1000"
            height="200"
            class="map"
            frameborder="0"></iframe>

    <Footer />

  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import Footer from "@/components/Footer";
export default {
  name: "Contacts",
  components: {
    Header,
    Footer
  },
}
</script>

<style>
.contacts{
  background-size: 100%;
}
.title{
  color: #00006f;
  padding-top: 2px;
  padding-bottom: 10px;
}
.left {
  float: left;
}
.center{
  margin-left: 435px;
  margin-right: auto;
  width: 1000px;
  margin-bottom: 30px;
}
.icon{
  background-color: #BDE0FF;
  text-align: center;
  vertical-align: middle;
  line-height: 70px;
}
.text{
  background-color: #D6ECFF;
  height: 70px;
  width: 600px;

}
.blockText{
  color: #000000;
  text-align: center;
  vertical-align: middle;
  line-height: 70px;
}
.map{
  margin-bottom: 30px
}
</style>