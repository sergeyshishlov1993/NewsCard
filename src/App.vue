<template>
  <div class="container pt-1">
    <div class="card">
      <!-- c помошью интерполяции выводим динамически текуюшую дату на страницу -->
      <h2>Актуальные новости {{ now }}</h2>
      <span>
        <strong>Открыто: {{ openRate }} | Прочитано {{ readRate }}</strong>
      </span>
    </div>
    <!-- используем компанент который мы импортировали и передаем в него ствойство prop, через цикл выводим содердимое массиыв на страницу -->
    <!-- с помошью директивы v-bind передаем props в компанент ребенка -->
    <!-- передаем событие которе полчаем от ребенка компанента для изменение счетчика  -->
    <AppNew
      :items="item.titel"
      :id="item.id"
      v-model="item.isOpen"
      :wasRead="item.wasRead"
      @open-news="openNews"
      @read-news="readNews"
      @unmark="removeNewsRead"
      v-for="item in news"
      :key="item.id"
    ></AppNew>

    <!-- 
    создаем блок который нам нужно повторить, проходимся по нему циклом v-for после чего за каждым элементом закрепляем уникальный индификатор через директиву :key 
    <div class="card" v-for="(item, i) in news" :key="item">
      выводим содержимое массива на странице который перебирает цикл второй параметр это индекс массива
      <h3>{{ item }} {{ i + 1 }}</h3>
      <button @click="isOpen = !isOpen" class="btn">Открыть</button>
      навешиваем обработчик события который при клике меняет параметр false на true
      <p v-if="isOpen">
        задаем директиву v if если параметр в false не показывать его на страницу 
        Lorem, ipsum dolor sit amet consectetur adipisicing elit. Inventore nam
        ducimus sunt enim quam maxime atque odit alias quos doloremque, nisi
        fugiat laborum officiis aspernatur ea. Eius iusto esse perspiciatis?
      </p>
    </div> -->
  </div>
</template>

<script>
import AppNew from "./componets/AppNew";
export default {
  data: () => ({
    openRate: 0,
    readRate: 0,
    now: new Date().toLocaleDateString(), //создаем метод обькта который будет нам возврашать текуюшую дату в нужном флормате с помощью toLocaleDateString
    news: [
      {
        titel: "Какая то новость на этой странице ",
        id: 1,
        isOpen: false,
        wasRead: false,
      },
      {
        titel: "Какая то новость на этой странице ",
        id: 2,
        isOpen: false,
        wasRead: false,
      },
      {
        titel: "Какая то новость на этой странице ",
        id: 3,
        isOpen: false,
        wasRead: false,
      },

      //создаем массив с какими то новостями которые мы планируем выводить на страницу
    ],
  }),
  provide: () => {
    return {
      titel: "golova",
      news: [
        {
          titel: "Какая то новость на этой странице ",
          id: 1,
          isOpen: false,
          wasRead: false,
        },
        {
          titel: "Какая то новость на этой странице ",
          id: 2,
          isOpen: false,
          wasRead: false,
        },
        {
          titel: "Какая то новость на этой странице ",
          id: 3,
          isOpen: false,
          wasRead: false,
        },

        //создаем массив с какими то новостями которые мы планируем выводить на страницу
      ],
    };
  },
  components: {
    AppNew,
  },
  methods: {
    openNews() {
      this.openRate++;
    },
    readNews(id) {
      const idx = this.news.findIndex((news) => news.id === id); //для того что бы удалять кнопку у новости , у каждой новости сравнивает что индекс массива должен совпадать с индексом который мы передаем из ребенка компанента
      this.news[idx].wasRead = true; //далее обрашаемся к массиву и к нужному индексу и меняем его значение с true на false
      this.readRate++;
    },
    removeNewsRead(id) {
      const news = this.news.find((news) => news.id === id);
      news.wasRead = false;
      this.readRate--;
    },
  },
};
</script>

<style lang="scss"></style>
