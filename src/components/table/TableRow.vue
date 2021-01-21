<template>
  <div class="table__body-container">
    <tr class="table__body-row table__body-row--main">
      <td
        class="table__body-item table__body-item--name"
        @click="toggleChildren()"
        :class="itemHasChildren"
        :style="{ marginLeft: this.indentMultiplier * this.depth + 'px' }"
      >
        {{ rowData.name }}
      </td>
      <td class="table__body-item table__body-item--phone">{{ rowData.phone_number }}</td>
    </tr>
    <tr class="table__body-row table__body-row--subordinates" v-if="showChildren">
      <TableRow
        v-for="(subordinate, index) in rowData.subordinates"
        :rowData="subordinate"
        :key="index"
        :depth="depth + depthCounter"
      ></TableRow>
    </tr>
  </div>
</template>

<script>
export default {
  name: 'TableRow',
  props: {
    rowData: Object,
    depth: Number
  },
  data: () => ({
    showChildren: false,
    indentMultiplier: 25,
    depthCounter: 1
  }),
  computed: {
    itemHasChildren() {
      return { 'has-children': this.rowData.subordinates.length }
    },
    indent() {
      return { marginLeft: `${this.depth * 1}px` }
    }
  },
  methods: {
    toggleChildren() {
      this.showChildren = !this.showChildren
    }
  }
}
</script>

<style>
td {
  box-shadow: 0 -1px 0 0 black;
}
/* .table__body > .table__body-container {
  box-shadow: 0 -1px 0 0 black;
} */
.table__body-row--main {
  justify-content: space-between;
  width: 100%;
  display: flex;
}
.table__body-item {
  text-align: center;
  text-align: left;
  box-sizing: border-box;
}
.table__body-item--name {
  position: relative;
  padding: 20px 20px 20px 22px;
  display: flex;
  flex-grow: 1;
}
.table__body-item--phone {
  padding: 20px 25px;
  flex-basis: 60%;
}
.table__body-row--subordinates {
  display: flex;
  flex-direction: column;
}
.table__body-row--subordinates > .table__body-container {
  justify-content: space-between;
  width: 100%;
  display: flex;
  flex-direction: column;
}
.has-children {
  cursor: pointer;
}
.has-children::before {
  content: '+';
  position: absolute;
  top: 35%;
  left: 4%;
  width: 20px;
  height: 20px;
}
</style>