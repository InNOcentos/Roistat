<template>
  <button class="add-btn btn" @click="tableModalOpenBtnClick">Добавить</button>
</template>

<script>
export default {
  name: 'AddUserButton',
  methods: {
    tableModalOpenBtnClick() {
      this.$emit('tableModalOpenBtnClick')
    }
  }
}
</script>

<style>
.add-btn {
  padding: 6px 27px;
  margin-bottom: 35px;
}
</style>