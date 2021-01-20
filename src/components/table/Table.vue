<template>
  <div class="table">
    <thead class="table__header">
      <tr class="table__header-row">
        <th class="table__header-item" @click="sortByName"><h3>Имя</h3></th>
        <th class="table__header-item" @click="sortByPhone"><h3>Телефон</h3></th>
      </tr>
    </thead>
    <tbody class="table__body">
      <TableRow v-for="(row, index) in usersData" :key="index" :rowData="row" :depth="0" />
    </tbody>
  </div>
</template>

<script>
import TableRow from '@/components/table/TableRow'

export default {
  name: 'Table',
  props: {
    usersData: Array
  },
  components: {
    TableRow
  },
  methods: {
    sortByName() {
      this.usersData.sort((a, b) => a.name.localeCompare(b.name))
    },
    sortByPhone() {
      this.usersData.sort((a, b) => a.phone.localeCompare(b.phone))
    }
  }
}
</script>

<style>
.table {
  min-width: 330px;
  max-width: 450px;
  width: 100%;
  border-collapse: collapse;
  border: 1px solid;
  border-bottom: 0;
  border-left: 0;
}
.table__header,
.table__body {
  display: flex;
  justify-content: space-between;
}
.table__body {
  flex-direction: column;
}
.table__header-row {
  width: 100%;
  display: flex;
}
.table__header-item {
  padding: 10px 0;
  font-weight: normal;
  text-align: left;
}
.table__header-item h3 {
  padding-left: 30px;
}
.table__header-item:first-child {
  flex-basis: 40%;
}
.table__header-item:nth-child(2) {
  flex-basis: 60%;
}
</style>