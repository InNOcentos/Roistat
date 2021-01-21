<template>
  <div class="addModal">
    <div class="addModal__heading">
      <h3>Добавление пользователя</h3>
      <span class="addModal__heading--close" @click="tableModalCloseBtnClick">x</span>
    </div>
    <form class="addModal__form" ref="addModal__form" @submit.prevent="sendFormValues">
      <div class="addModal__form-item">
        <label for="name">Имя</label>
        <input type="text" name="name" />
      </div>
      <div class="addModal__form-item">
        <label for="phone">Телефон</label>
        <input type="text" name="phone" />
      </div>
      <div class="addModal__form-item">
        <label for="chief">Начальник</label>
        <select v-model="parsedUsersDataCopy" name="chief">
          <option :value="item.id" v-for="(item, index) in parsedUsersData" :key="index">{{ item.name }}</option>
        </select>
      </div>
      <input type="submit" class="btn save-btn" value="Отправить" />
    </form>
  </div>
</template>

<script>
export default {
  name: 'AddUserModal',
  props: {
    parsedUsersData: Array
  },
  data: () => ({
    parsedUsersDataCopy: this.parsedUsersData
  }),
  methods: {
    tableModalCloseBtnClick() {
      this.$emit('tableModalCloseBtnClick')
    },
    sendFormValues(e) {
      this.$emit('tableModalSaveBtnClick', {
        name: e.target.elements.name.value,
        phone_number: e.target.elements.phone.value,
        chiefId: e.target.elements.chief.value
      })
      this.$refs.addModal__form.reset()
    }
  },
  computed: {}
}
</script>

<style>
.addModal {
  position: absolute;
  right: -175%;
  top: 64px;
  width: 95%;
  height: 360px;
  border: 1px solid;
  padding: 15px 25px;
  text-align: left;
}
.addModal__heading {
  display: flex;
  justify-content: space-between;

  margin-bottom: 40px;
}
.addModal__heading--close {
  cursor: pointer;
}
.addModal__form {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.addModal__form-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}
.addModal__form-item + .addModal__form-item {
  margin-top: 30px;
}
.addModal__form-item input,
.addModal__form-item select {
  padding: 8px;
  outline: none;
  width: 240px;
}
.addModal__form-item select {
  border-radius: 6px;
}
.save-btn {
  text-align: left;
  padding: 9px 85px 9px 21px;

  margin-top: 30px;
}
</style>