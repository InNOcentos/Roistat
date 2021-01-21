<template>
  <div class="table-section">
    <UserAddButton @tableModalOpenBtnClick="showTableModal" @click="getParsedUsersData"></UserAddButton>
    <div class="table">
      <thead class="table__header">
        <tr class="table__header-row">
          <th class="table__header-item" @click="sortByName"><h3>Имя</h3></th>
          <th class="table__header-item" @click="sortByPhone"><h3>Телефон</h3></th>
        </tr>
      </thead>
      <tbody class="table__body">
        <TableRow v-for="(row, index) in getUsersData" :key="index" :rowData="row" :depth="0" />
      </tbody>
    </div>
    <UserModal
      v-if="tableModalIsVisible"
      :parsedUsersData="parsedUsersData"
      @tableModalCloseBtnClick="closeTableModal"
      @tableModalSaveBtnClick="saveTableModalData"
    ></UserModal>
  </div>
</template>

<script>
import TableRow from '@/components/table/TableRow'
import UserModal from '@/components/table/modal/UserModal'
import UserAddButton from '@/components/table/modal/UserAddButton'

export default {
  name: 'Table',
  props: {
    usersData: Array
  },
  components: {
    TableRow,
    UserModal,
    UserAddButton
  },
  data: () => ({
    tableModalIsVisible: false,
    parsedUsersData: []
  }),
  computed: {
    getParsedUsersData() {
      this.parsedUsersData.length = 0
      return this.parseArrayData(this.getUsersData)
    },
    getParsedUsersDataLength() {
      return this.parsedUsersData.length
    },
    getUsersData() {
      return JSON.parse(localStorage.getItem('usersData')) || this.usersData
    }
  },
  watch: {
    usersData(newUsersData, oldUsersData) {
      localStorage.setItem('usersData', JSON.stringify(this.usersData))
    }
  },
  methods: {
    sortByName() {
      this.getUsersData.sort((a, b) => a.name.localeCompare(b.name))
    },
    sortByPhone() {
      this.getUsersData.sort((a, b) => a.phone.localeCompare(b.phone))
    },
    showTableModal() {
      this.tableModalIsVisible = true
    },
    closeTableModal() {
      this.tableModalIsVisible = false
    },
    saveDataToLocalStorage() {
      localStorage.setItem('usersData', JSON.stringify(this.getUsersData))
    },
    parseArrayData(array) {
      return array.map((e) => {
        this.parsedUsersData.push(e)
        if (e.subordinates) {
          this.parseArrayData(e.subordinates)
        }
      })
    },
    saveTableModalData(value) {
      const newTableModalData = {
        id: this.getParsedUsersDataLength + 1,
        name: value.name,
        phone_number: value.phone,
        subordinates: []
      }

      this.getUsersData.forEach((e, index) => {
        if (e.id === +value.chiefId) {
          e.subordinates.push(newTableModalData)
        }
        while (e.subordinates.length) {
          if (e.subordinates[0].id === +value.chiefId) {
            e.subordinates[0].subordinates.push(newTableModalData)
          }
          e = e.subordinates[0]
        }
      })
      this.saveDataToLocalStorage()
    }
  }
}
</script>

<style>
.table-section {
  text-align: right;
  max-width: 450px;
  width: 100%;
  position: relative;
}
.table {
  min-width: 330px;
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

.btn {
  border-radius: 8px;
  border: 1px solid;
  background-color: rgba(0, 0, 0, 0.15);
  outline: none;
  cursor: pointer;
}
</style>