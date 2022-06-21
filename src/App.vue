<template>
  <div class="container">
    <div class="courses">
      <span>Courses</span>
      <div class="courses__param">
        <div class="courses__param-min">
          Min price: <input v-model="minPrice" />
        </div>
        <div class="courses__param-max">
          Max price: <input v-model="maxPrice" />
        </div>
        <div class="courses__buttons">
          <button
            @click="buttonReset"
            class="courses__param-reset courses__button"
          >
            Сбросить
          </button>
          <select v-model="paramSelect" class="courses__param-select">
            <option disabled value="">Сортировать по</option>
            <option value="1">По возрастанию цены</option>
            <option value="2">По убыванию цены</option>
          </select>
        </div>
      </div>
      <div class="courses__list">
        <div
          v-for="course in courses"
          :key="course.name"
          class="coursers__list-item"
        >
          <div
            v-if="
              (course.prices[0] >= minPrice || course.prices[0] == null) &&
              (course.prices[1] - maxPrice <= 0 ||
                course.prices[1] == null ||
                maxPrice == '')
            "
          >
            <label> {{ course.name }}:</label>
            <label>
              {{ "" + course.prices[0] }} - {{ "" + course.prices[1] }}</label
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      courses: [
        { name: "Courses in England", prices: [0, 100] },
        { name: "Courses in Germany", prices: [500, null] },
        { name: "Courses in Italy", prices: [100, 200] },
        { name: "Courses in Russia", prices: [null, 400] },
        { name: "Courses in China", prices: [50, 250] },
        { name: "Courses in USA", prices: [200, null] },
        { name: "Courses in Kazakhstan", prices: [56, 324] },
        { name: "Courses in France", prices: [null, null] },
        { name: "Courses in France", prices: [null, 14] },
      ],
      minPrice: "",
      maxPrice: "",
      paramSelect: "",
    };
  },

  methods: {
    buttonReset() {
      this.minPrice = "";
      this.maxPrice = "";
    },
    sortCourses(a, b) {
      if (this.paramSelect == 1) {
        if (a.prices[0] == null) return 1;
        if (b.prices[0] == null) return -1;
        if (a.prices[0] > b.prices[0]) return 1;
        if (a.prices[0] == b.prices[0]) return 0;
        if (a.prices[0] < b.prices[0]) return -1;
      } else if (this.paramSelect == 2) {
        if (a.prices[1] == null) return 1;
        if (b.prices[1] == null) return -1;
        if (a.prices[1] > b.prices[1]) return -1;
        if (a.prices[1] == b.prices[1]) return 0;
        if (a.prices[1] < b.prices[1]) return 1;
      }
    },
  },

  watch: {
    paramSelect() {
      this.courses.sort(this.sortCourses);
    },
  },
};
</script>

<style></style>
