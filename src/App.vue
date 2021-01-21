<template>
  <div id="app">
    <Table :usersData="usersData" />
  </div>
</template>

<script>
import Table from '@/components/table/Table'

export default {
  name: 'App',
  components: {
    Table
  },
  data: () => ({
    usersData: [
      {
        id: 1,
        name: 'Марина',
        phone_number: '+7 941 123 21 42',
        subordinates: []
      },
      {
        id: 2,
        name: 'Петр',
        phone_number: '+7 941 123 21 42',
        subordinates: []
      },
      {
        id: 3,
        name: 'Алексей',
        phone_number: '+7 941 123 21 42',
        subordinates: [
          {
            id: 4,
            name: 'Иван',
            phone_number: '+7 941 123 21 42',
            subordinates: [
              {
                id: 5,
                name: 'Василий',
                phone_number: '+7 941 123 21 42',
                subordinates: []
              }
            ]
          }
        ]
      },
      {
        id: 6,
        name: 'Борис',
        phone_number: '+7 941 123 21 42',
        subordinates: []
      }
    ]
  })
}
</script>

<style>
* {
  box-sizing: border-box;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
body {
  margin: 35px 100px;
}
h3 {
  font-weight: normal;
  margin: 0;
  font-size: inherit;
}
th,
td {
  border: 1px solid;
  border-top: 0;
  border-right: 0;
}
</style>
