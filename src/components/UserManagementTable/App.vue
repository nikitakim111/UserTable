<template>
  <div>
    <UserFormModal v-if="showModal" @closeModal="closeModal" :users="users"></UserFormModal>

    <button @click="showModal = true" class="addUserBtn">Добавить пользователя</button>

    <div class="table">

      <div class="header-row">
        <span class="header-cell">ID</span>
        <span class="header-cell">Имя</span>
        <span class="header-cell">Телефон</span>
        <span class="header-cell">ID Родителя</span>
      </div>

      <div class="userlist-row">
        <UserList :users="users" />
      </div>

    </div>
  </div>
</template>

<script>
import UserFormModal from '../UserFormModal/App.vue'
import UserList from './UserList.vue'

export default {

  components: {
    UserFormModal,
    UserList,
  },

  data () {
    return {
      users: [],
      showModal: false
    }
  },

  mounted () {
    const localStorageData = localStorage.getItem('users')
    if (localStorageData) {
      this.users = JSON.parse(localStorageData)
    }
  },

  methods: {

    closeModal () {
      this.showModal = !this.showModal
    }

  }
}
</script>

<style scoped>
.addUserBtn {
  margin-bottom: 20px;
}

.table {
  display: grid;
  grid-template-rows: 50px auto;
}

.header-row {
  grid-column: 1 / 3;
  display: flex;
}

.header-cell {
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: Arial;
  border: 1px solid black;
  background-color: #f0f0f0;
  width: 25%;
  font-weight: bold;
  font-size: 16px;
}

.header-cell:last-child {
  width: 26%;
}

.userlist-row {
  grid-column: 1 / 3;
}

</style>
