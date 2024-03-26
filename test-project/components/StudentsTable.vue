<script lang="js">
export default {
  data() {
    return {
      studentsList: [],
      searchQuery: '',
      currentPage: 1,
      itemsInPage: 5,
      filter: []
    };
  },
  computed: {
    totalPagesForStudent() {
      return Math.ceil(this.filter.length / this.itemsInPage);
    },
    paginatedAllStudents() {
      const startIndex = (this.currentPage - 1) * this.itemsInPage;
      const endIndex = startIndex + this.itemsInPage;
      return this.filter.slice(startIndex, endIndex);
    }
  },
  methods: {
    previousPageForStudent() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    nextPageForStudent() {
      if (this.currentPage < this.totalPagesForStudent) {
        this.currentPage++;
      }
    },
    searchForStudent() {
      this.filter = this.studentsList.filter(student =>
          student.firstName.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          student.lastName.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          student.group.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
      this.currentPage = 1;
    }
  },
  mounted() {
    this.studentsList =[
      { id: 1, firstName: 'Тарас', lastName: 'Петров', group: 'Група 1' },
      { id: 2, firstName: 'Олексій', lastName: 'Іванов', group: 'Група 1' },
      { id: 3, firstName: 'Марія', lastName: 'Сидорова', group: 'Група 1' },
      { id: 4, firstName: 'Андрій', lastName: 'Федоренко', group: 'Група 1' },
      { id: 5, firstName: 'Юлія', lastName: 'Коваленко', group: 'Група 1' },

      { id: 6, firstName: 'Петро', lastName: 'Козак', group: 'Група 2' },
      { id: 7, firstName: 'Олена', lastName: 'Семененко', group: 'Група 2' },
      { id: 8, firstName: 'Ігор', lastName: 'Павленко', group: 'Група 2' },
      { id: 9, firstName: 'Анастасія', lastName: 'Литвин', group: 'Група 2' },
      { id: 10, firstName: 'Олег', lastName: 'Мельник', group: 'Група 2' },

      { id: 11, firstName: 'Анна', lastName: 'Шевченко', group: 'Група 3' },
      { id: 12, firstName: 'Василь', lastName: 'Ковальчук', group: 'Група 3' },
      { id: 13, firstName: 'Наталія', lastName: 'Жук', group: 'Група 3' },
      { id: 14, firstName: 'Віталій', lastName: 'Панасенко', group: 'Група 3' },
      { id: 15, firstName: 'Тетяна', lastName: 'Лисенко', group: 'Група 3' },

      { id: 16, firstName: 'Дмитро', lastName: 'Григоренко', group: 'Група 4' },
      { id: 17, firstName: 'Катерина', lastName: 'Кузьменко', group: 'Група 4' },
      { id: 18, firstName: 'Євген', lastName: 'Ткаченко', group: 'Група 4' },
      { id: 19, firstName: 'Ольга', lastName: 'Бондаренко', group: 'Група 4' },
      { id: 20, firstName: 'Максим', lastName: 'Мартиненко', group: 'Група 4' },

      { id: 21, firstName: 'Сергій', lastName: 'Кравченко', group: 'Група 5' },
      { id: 22, firstName: 'Єлизавета', lastName: 'Романенко', group: 'Група 5' },
      { id: 23, firstName: 'Дарина', lastName: 'Гриценко', group: 'Група 5' },
      { id: 24, firstName: 'Євгенія', lastName: 'Морозенко', group: 'Група 5' },
      { id: 25, firstName: 'Роман', lastName: 'Поляков', group: 'Група 5' },

      { id: 26, firstName: 'Марина', lastName: 'Кравчук', group: 'Група 6' },
      { id: 27, firstName: 'Артем', lastName: 'Сорокін', group: 'Група 6' },
      { id: 28, firstName: 'Діана', lastName: 'Литвиненко', group: 'Група 6' },
      { id: 29, firstName: 'Олександра', lastName: 'Тимошенко', group: 'Група 6' },
      { id: 30, firstName: 'Володимир', lastName: 'Захаренко', group: 'Група 6' },

      { id: 31, firstName: 'Євгеній', lastName: 'Мірошніченко', group: 'Група 7' },
      { id: 32, firstName: 'Аліна', lastName: 'Павлюченко', group: 'Група 7' },
      { id: 33, firstName: 'Михайло', lastName: 'Лукянчук', group: 'Група 7' },
      { id: 34, firstName: 'Оксана', lastName: 'Литвинова', group: 'Група 7' },
      { id: 35, firstName: 'Ірина', lastName: 'Бондаренко', group: 'Група 7' },

      { id: 36, firstName: 'Вікторія', lastName: 'Шевченко', group: 'Група 8' },
      { id: 37, firstName: 'Євгенія', lastName: 'Кузьміна', group: 'Група 8' },
      { id: 38, firstName: 'Ілля', lastName: 'Гордієнко', group: 'Група 8' },
      { id: 39, firstName: 'Нікіта', lastName: 'Лисенко', group: 'Група 8' },
      { id: 40, firstName: 'Олександра', lastName: 'Ткачук', group: 'Група 8' },

      { id: 41, firstName: 'Андріана', lastName: 'Ковальчук', group: 'Група 9' },
      { id: 42, firstName: 'Євгенія', lastName: 'Сидоренко', group: 'Група 9' },
      { id: 43, firstName: 'Станіслав', lastName: 'Мельник', group: 'Група 9' },
      { id: 44, firstName: 'Наталія', lastName: 'Петренко', group: 'Група 9' },
      { id: 45, firstName: 'Руслан', lastName: 'Шевчук', group: 'Група 9' },

      { id: 46, firstName: 'Маргарита', lastName: 'Козаченко', group: 'Група 10' },
      { id: 47, firstName: 'Олексій', lastName: 'Даниленко', group: 'Група 10' },
      { id: 48, firstName: 'Софія', lastName: 'Кравченко', group: 'Група 10' },
      { id: 49, firstName: 'Максим', lastName: 'Гриценко', group: 'Група 10' },
      { id: 50, firstName: 'Олена', lastName: 'Морозова', group: 'Група 10' }
    ]
        this.filter = this.studentsList;
  }
};
</script>
<template>
  <div>
    <h1 class="text-2xl text-center m-5 text-black-500">Список студентів</h1>
    <div class="mb-4">
      <input type="text" v-model="searchQuery" @input="searchForStudent" placeholder="Пошук студента" class="bg-gray-200 py-2 px-4 rounded-lg focus:outline-none focus:shadow-outline w-50" style="margin-bottom: 10px; color:black;">
      <table class="w-full table-fixed">
        <thead>
        <tr>
          <th class="bg-gray-100 border border-gray-300 py-2">Ім'я</th>
          <th class="bg-gray-100 border border-gray-300 py-2">Прізвище</th>
          <th class="bg-gray-100 border border-gray-300 py-2">Група</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="student in paginatedAllStudents" :key="student.id" class="border border-gray-300 hover:bg-gray-200">
          <td class="border border-gray-300 py-2">{{ student.firstName }}</td>
          <td class="border border-gray-300 py-2">{{ student.lastName }}</td>
          <td class="border border-gray-300 py-2">{{ student.group }}</td>
        </tr>
        </tbody>
      </table>
    </div>

    <button @click="previousPageForStudent" :disabled="currentPage === 1" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mr-2">
      <
    </button>
    <span class="text-gray-500"> {{ currentPage }} з {{ totalPagesForStudent }}</span>
    <button @click="nextPageForStudent" :disabled="currentPage === totalPagesForStudent" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded ml-2">
      >
    </button>
  </div>
</template>

<style scoped>

</style>