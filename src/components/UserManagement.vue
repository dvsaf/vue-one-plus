<template>
  <div id="user-management" class="row pt-3 pb-3">
    <div class="col-3 bg-light">
      <div class="filter-block">
        <div class="filer-block-header">Выбрано</div>
        <div class="filer-block-content">
          <div v-if="filters.username"><strong>Логин: </strong>{{ filters.username }}</div>
          <div v-if="filters.lastName"><strong>Фамилия: </strong>{{ filters.lastName }}</div>
          <div v-if="filters.email"><strong>Email: </strong>{{ filters.email }}</div>
<!--          <div v-if="filters.college"><strong>ПОО: </strong>{{ filters.college.shortName }}</div>-->
          <div class="row">
            <b-button class="col ml-3 mr-1" @click="clearFilters">Очистить</b-button>
            <b-button class="col ml-1 mr-3" @click="findFiltered">Найти</b-button>
          </div>
        </div>
      </div>
      <div class="filter-block filter-block-collapsable">
        <div class="filer-block-header">Основная информация</div>
        <div class="filer-block-content">
          <div>
            <label for="login">Логин</label>
            <input id="login" type="text" class="form-control" v-model="filters.username">
          </div>
          <div>
            <label for="last-name">Фамилия</label>
            <input id="last-name" type="text" class="form-control" v-model="filters.lastName">
          </div>
          <div>
            <label for="email">Email</label>
            <input id="email" type="text" class="form-control" v-model="filters.email">
          </div>
<!--          <div>-->
<!--            <label :for="`college`">ПОО</label>-->
<!--            <b-form-input :id="`college`" class="form-control" list="colleges" v-model="selectedCollege"-->
<!--                          @change="changeCollege"></b-form-input>-->
<!--            <datalist id="colleges">-->
<!--              <option v-for="college in colleges" v-bind:key="college.id">{{ college.shortName }}</option>-->
<!--            </datalist>-->
<!--          </div>-->
        </div>
      </div>
    </div>
    <div class="col-9">
      <b-table ref="usersTable" id="users" striped hover :items="userProvider" :fields="userFields" primary-key="id"
               :per-page="perPage"
               :current-page="currentPage">
        <template v-slot:cell(actions)="data">
          <b-button class="btn btn-sm">{{ data.item.id }}</b-button>
        </template>
        <template v-slot:cell()="data">
          {{ data.value }}
        </template>
      </b-table>
      <p class="mt-3">Страница: {{ currentPage }}</p>
      <b-pagination v-model="currentPage" :total-rows="rows" :per-page="perPage" aria-controls="users"
                    align="center"></b-pagination>
    </div>
  </div>
</template>

<script>
// const collegesUrl = "http://localhost:9081/colleges";
const usersListUrl = "http://localhost:9001/users/list";
const usersCountUrl = "http://localhost:9001/users/count";

// function fetchColleges(self) {
//   const xhr = new XMLHttpRequest();
//   xhr.open("GET", collegesUrl);
//   xhr.onload = function () {
//     self.colleges = JSON.parse(xhr.responseText);
//   };
//   xhr.send();
// }

function fetchUsersCount(self, filters) {
  const xhr = new XMLHttpRequest();
  const url = usersCountUrl + "?" + getFiltersUrl(filters); // todo: заменить на аггрегацию
  xhr.open("GET", url);
  xhr.setRequestHeader("Authorization", "Bearer " + localStorage.jwtProfteh);
  xhr.onload = function () {
    self.rows = JSON.parse(xhr.responseText);
    console.log("rows = " + self.rows);
  };
  xhr.send();
}

function getFiltersUrl(filters) {
  return (filters.username == null ? "" : "&username=" + filters.username)
      + (filters.lastName == null ? "" : "&last-name=" + filters.lastName)
      + (filters.email == null ? "" : "&email=" + filters.email)
      // + (filters.college == null ? "" : "&college=" + filters.college.id)
      ;
}

function fetchUsers(currentPage, perPage, filters, callback) {
  const xhr = new XMLHttpRequest();
  const url = usersListUrl + '?page=' + currentPage + '&size=' + perPage
      + getFiltersUrl(filters);
  xhr.open("GET", url);
  xhr.setRequestHeader("Authorization", "Bearer " + localStorage.jwtProfteh);
  xhr.onload = function () {
    let users = JSON.parse(xhr.responseText);
    callback(users);
  };
  xhr.send();
}

export default {
  name: "UserManagement",

  data() {
    return {
      filters: {
        username: null,
        lastName: null,
        email: null,
        // college: null,
        active: true,
        banned: null
      },
      activeFilters: [],
      // selectedCollege: null,
      // colleges: [],
      userFields: [
        {key: 'username', label: 'Логин', sortable: true},
        {key: 'lastName', label: 'ФИО', sortable: true},
        {key: 'roles', label: 'Роли', sortable: false},
        {key: 'actions', label: '', sortable: false}
      ],
      rows: 0,
      perPage: 7,
      currentPage: 1
    }
  },

  created() {
    // fetchColleges(this);
    fetchUsersCount(this, this.filters);
  },

  methods: {
    clearFilters() {
      this.filters.username = null;
      this.filters.lastName = null;
      this.filters.email = null;
      this.filters.college = null;
      this.filters.active = true;
      this.filters.banned = null;
      // this.selectedCollege = null;
    },

    // changeCollege(value) {
    //   this.filters.college = this.colleges.find((item) => {
    //     return item.shortName === value;
    //   });
    // },

    userProvider(ctx, callback) {
      fetchUsers(ctx.currentPage, ctx.perPage, this.filters, callback);

      // Must return null or undefined to signal b-table that callback is being used
      return null;
    },

    findFiltered() {
      fetchUsersCount(this, this.filters);
      this.$refs.usersTable.refresh();
    }
  }
}
</script>

<style scoped>

</style>