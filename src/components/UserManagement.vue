<template>
  <div id="user-management">
    <div class="filter-block">
      <div class="filer-block-header">Выбрано</div>
      <div class="filer-block-content">
        <div v-if="filters.login"><strong>Логин: </strong>{{ filters.login }}</div>
        <div v-if="filters.lastName"><strong>Фамилия: </strong>{{ filters.lastName }}</div>
        <div v-if="filters.email"><strong>Email: </strong>{{ filters.email }}</div>
<!--        <div v-if="filters.college"><strong>ПОО: </strong>{{ filters.college.name }}</div>-->
        <div class="btn btn-primary" onclick="userManagement.clearFilters()">Очистить</div>
        <div class="btn btn-primary">Найти</div>
      </div>
    </div>
    <div class="filter-block filter-block-collapsable">
      <div class="filer-block-header">Основная информация</div>
      <div class="filer-block-content">
        <div>
          <label for="login">Логин</label>
          <input id="login" v-model="filters.login">
        </div>
        <div>
          <label for="last-name">Фамилия</label>
          <input id="last-name" v-model="filters.lastName">
        </div>
        <div>
          <label for="email">Email</label>
          <input id="email" v-model="filters.email">
        </div>
<!--        <div>-->
<!--          <label for="college">ПОО</label>-->
<!--          <p-autocomplete id="college" v-model="selectedCollege" :dropdown="true" :suggestions="filteredColleges"-->
<!--                          @complete="searchCollege($event)" @item-select="selectCollege()" @clear="clearCollege()"-->
<!--                          field="name"></p-autocomplete>-->
<!--        </div>-->
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserManagement",

  data() {
    return {
      filters: {
        login: null,
        lastName: null,
        email: null,
        college: null,
        active: true,
        banned: null
      },
      activeFilters: [],
      users: [],
      colleges: [
        {id: 1, name: 'aaa'},
        {id: 2, name: 'bbb'},
        {id: 3, name: 'ccc'},
        {id: 4, name: 'sad'},
        {id: 5, name: 'awe'},
        {id: 6, name: 'era'}],
      filteredColleges: [],
      selectedCollege: null
    }
  },

  methods: {
    clearFilters() {
      this.filters.login = null;
      this.filters.lastName = null;
      this.filters.email = null;
      this.filters.college = null;
      this.filters.active = true;
      this.filters.banned = null;
    },

    searchCollege(event) {
      this.filteredColleges = this.colleges.filter((college) => {
        return college.name.toLowerCase().indexOf(event.query.toLowerCase()) >= 0
      });
    },

    selectCollege() {
      this.filters.college = this.selectedCollege;
    },

    clearCollege() {
      this.filters.college = null;
    }
  }
}
</script>

<style scoped>

</style>