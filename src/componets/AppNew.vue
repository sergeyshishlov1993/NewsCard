<template>
  <!-- создваем ребенка компонента с карточками что бы при открытии новости каждая карточка открывлась отдельно, а не все сразу -->
  <div class="card">
    <!-- передаем в шаблон props который мы получилит от родителя  -->
    <h3>{{ id }} {{ items }}</h3>
    <!-- на кнопки навешиваем событие клик который при клике будет вызывать метод  -->
    <button @click="open" class="btn">Открыть</button>
    <!-- в зависимости от значение свойства будем показывать или скрывать блок  -->
    <p v-if="isNewOpen">
      Lorem, ipsum dolor sit amet consectetur adipisicing elit. Inventore nam
      ducimus sunt enim quam maxime atque odit alias quos doloremque, nisi
      fugiat laborum officiis aspernatur ea. Eius iusto esse perspiciatis?
    </p>
  </div>
</template>

<script>
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
  },
};
</script>
