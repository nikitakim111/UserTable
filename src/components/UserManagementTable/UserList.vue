<template>
  <div class="user-list">

    <div v-for="user in users" :key="user.id" :style="{ paddingLeft: isTopLevel(user) ? '0' : '2rem' }"
      class="user">

      <ul class="user-info">
        <li class="user-info-item">{{ user.id }}</li>
        <li class="user-info-item">{{ user.name }}</li>
        <li class="user-info-item">{{ user.tel }}</li>
        <li class="user-info-item">{{ user.parentId }}</li>
        <li @click="toggleOpen(user.id)" class="user-info-item">
          <span v-if="hasChildren(user)" class="user-dropdown-btn">
            {{ isOpen(user.id) ? '-' : '+' }}
          </span>
        </li>
      </ul>

      <div v-if="isOpen(user.id)" class="user-children">
        <UserList :users="user.children" :open-ids="openIds" />
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'UserList',

  props: {
    users: {
      type: Array,
      required: true,
    },

    openIds: {
      type: Array,
      default: () => [],
    },
  },

  methods: {
    hasChildren (user) {
      return user.children && user.children.length
    },

    isOpen (id) {
      return this.openIds.includes(id)
    },

    isTopLevel (user) {
      const clonedUser = this.deepCloneObject(user)
      return clonedUser.parentId === null
    },

    toggleOpen (id) {
      if (this.isOpen(id)) {
        this.openIds.splice(this.openIds.indexOf(id), 1)
      } else {
        this.openIds.push(id)
      }
    },

    deepCloneObject (obj) {
      return JSON.parse(JSON.stringify(obj))
    },
  },

}
</script>

<style scoped>
.user:hover {
  background-color: lightblue;
}

.user-info {
  display: flex;
}

.user-children:first-child {
  background-color: red;
}

.user-info-item {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 5px 0;
  width: 25%;
  border-bottom: 1px solid black;
  border-left: 1px solid black;
  font-weight: bold;
  font-size: 16px;
  font-family: Arial;
}

.user-info-item:last-child {
  width: 17px;

}

.user-dropdown-btn {
  cursor: pointer;
}</style>
