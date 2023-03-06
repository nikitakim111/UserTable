<template>
  <form @submit.prevent="submitForm()" class="form">
    <form-group name="name" label="Имя" required />
    <form-group name="tel" label="Телефон" type="number" required />
    <form-group name="parent" label="Родитель" :options="getUsersWithOptions">
    </form-group>
      <button type="submit">Сохранить</button>
  </form>
</template>

<script>
import FormGroup from './formGroup.vue'

export default {
  components: {
    FormGroup,
  },
  props: {
    users: {
      type: Array,
      required: true,
    },
  },

  computed: {
    getUsersWithOptions () {
      const OPTIONS = []
      const processUser = (user) => {
        OPTIONS.push(user)
        if (user.children) {
          user.children.forEach(child => {
            processUser(child)
          })
        }
      }

      this.users.forEach(user => {
        processUser(user)
      })

      return OPTIONS
    }
  },

  methods: {
    submitForm () {
      const FORM_DATA = new FormData(this.$el)
      const PARENT_ID = FORM_DATA.get('parent')

      const USER_OBJ = {
        name: FORM_DATA.get('name'),
        tel: FORM_DATA.get('tel'),
        parentId: PARENT_ID || null,
        id: this.generateUserId(),
        children: [],
      }

      if (PARENT_ID) {
        const PARENT_USER = this.findUserById(PARENT_ID)

        PARENT_USER.children.push(USER_OBJ)
      } else {
        this.users.push(USER_OBJ)
      }

      localStorage.setItem('users', JSON.stringify(this.users))
    },

    generateUserId () {
      let id

      do {
        id = Math.floor(Math.random() * 100000).toString().padStart(5, '0')
      }
      while (this.users.some(user => user.id === id))

      return id
    },

    findUserById (id, users = this.users) {
      for (const USER of users) {
        if (USER.id === id) {
          return USER
        }

        if (USER.children) {
          const CHILD_USER = this.findUserById(id, USER.children)

          if (CHILD_USER) {
            return CHILD_USER
          }
        }
      }

      return null
    },

  },
}
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  align-items: self-end;
}

.form-group:not(:last-child) {
  margin-bottom: 10px;
}
</style>
