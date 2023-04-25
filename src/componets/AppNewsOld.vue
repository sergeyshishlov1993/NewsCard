<template>
  <!-- создваем ребенка компонента с карточками что бы при открытии новости каждая карточка открывлась отдельно, а не все сразу -->
  <div class="card">
    <!-- передаем в шаблон props который мы получилит от родителя  -->
    <h3>{{ id }} {{ items }}</h3>
    <!-- на кнопки навешиваем событие клик который при клике будет вызывать метод  -->
    <app-button @action="open">
      {{ isNewOpen ? "Закрыть" : "Открыть" }}
    </app-button>
    <!-- в зависимости от значение свойства будем показывать или скрывать блок  -->
    <div v-if="isNewOpen">
      <p>
        Lorem, ipsum dolor sit amet consectetur adipisicing elit. Inventore nam
        ducimus sunt enim quam maxime atque odit alias quos doloremque, nisi
        fugiat laborum officiis aspernatur ea. Eius iusto esse perspiciatis?
      </p>
      <hr />
      <app-button color="primary" v-if="!wasRead" @action="readNews">
        Прочесть новость
      </app-button>
      <!-- используем кастомный тег в котором мы указываем параметр color который мы передаем ребенку компаненту в качестве название класса который нужно добавить элементу  и слушаем событие которое мы кастомно переддали от ребенка компанента -->
      <app-button color="danger" @action="removeNews" v-if="wasRead">
        Отметить непрочитаные
      </app-button>
      <AppNewsList></AppNewsList>
    </div>
  </div>
</template>

<script>
import AppButton from "./AppButton.vue";
import AppNewsList from "./AppNewsList.vue";
export default {
  data: () => ({
    // isOpen: false,
    isNewOpen: !"item.isOpen",
    // по сколько на прямую ребенок компонент не может изменять родительский создаем новое свойство куда передаем props от родительского компанента
  }),
  props: {
    //валидируем props который хотим получить от родителя
    items: {
      type: String,
      requied: true,
    },
    id: Number,
    // isOpen: {
    //   type: Boolean,
    //   requied: false,
    //   default: false,
    //   valiator(value) {
    //     return value === true || value === false;
    //   },
    // },
    "item.IsOpen": Boolean,
    wasRead: Boolean,
  },
  emits: {
    "open-news": null,
    "read-news"(id) {
      if (id) {
        return true;
      }
      console.warn("нет обязательно параметра id");
      return false;
    },
    unmark(id) {
      if (id) {
        return true;
      }
      console.warn("нет обязательно параметра id");
      return false;
    },
  },
  methods: {
    open() {
      // в методах изменяем булевое значение на противоположное что бы скрыть или показывать блок
      this.isNewOpen = !this.isNewOpen;
      //   возрашаем событие в родительский блок что бы в нем изменять значение счетчика при клике на кнопку
      if (this.isNewOpen) {
        this.$emit("open-news");
      }
    },
    readNews() {
      this.isNewOpen = !this.isNewOpen;
      this.$emit("read-news", this.id);
    },
    removeNews() {
      this.$emit("unmark", this.id);
    },
  },
  components: {
    AppButton,
    AppNewsList,
  },
};
</script>
