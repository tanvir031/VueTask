<template>
  <div class="table-container">
    <table>
      <thead>
        <tr>
          <th rowspan="2" class="sticky-col">SL</th>
          <th rowspan="2" class="sticky-col">Member Id</th>
          <th rowspan="2" class="sticky-col">Name</th>
          <th rowspan="2" class="sticky-col">D/W/M passed</th>
          <th colspan="1" class="sticky-col">C</th>
          <th rowspan="2" class="sticky-col">A/c No</th>
          <th rowspan="2" class="sticky-col">Loan</th>
          <th rowspan="2" class="sticky-col">Gs</th>
          <th rowspan="2" class="sticky-col">VS</th>
          <th rowspan="2" class="sticky-col">DPS</th>
          <th colspan="3">Loan Collection Split</th>
          <th colspan="3">Loan Recoverable</th>
          <th colspan="2">Due / Advance</th>
          <th colspan="3">Loan Balance</th>
          <th rowspan="2">Disbursed Date</th>
          <th rowspan="2">Disbursed Amount</th>
          <th rowspan="2">GS PA Balance</th>
          <th rowspan="2">VS PA Balance</th>
          <th rowspan="2">View</th>
        </tr>
        <tr>
          <th class="sticky-col2">
            <input type="checkbox" v-model="selectAll" @change="toggleAll" />
          </th>
          <th>PA</th>
          <th>SC</th>
          <th>Total</th>
          <th>PA</th>
          <th>SC</th>
          <th>Total</th>
          <th>New Due</th>
          <th>Closing Due</th>
          <th>PA</th>
          <th>SC</th>
          <th>Total</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="(row, i) in data" :key="i" :class="{ edited: row.touched }">
          <td class="sticky-col">{{ row.sl }}</td>
          <td class="sticky-col">{{ row.memberId }}</td>
          <td class="sticky-col">{{ row.name }}</td>
          <td class="sticky-col">{{ row.dwmPassed }}</td>
          <td class="sticky-col">
            <input type="checkbox" v-model="row.selected" @change="markTouched(row)" />
          </td>
          <td class="sticky-col">
            <input v-model="row.acNo" @input="markTouched(row)" type="text" />
          </td>
          <td class="sticky-col">
            <input v-model="row.loan" @input="markTouched(row)" type="text" />
          </td>
          <td class="sticky-col">
            <input v-model="row.gs" @input="markTouched(row)" type="text" />
          </td>
          <td class="sticky-col">
            <input v-model="row.vs" @input="markTouched(row)" type="text" />
          </td>
          <td class="sticky-col">
            <input v-model="row.dps" @input="markTouched(row)" type="text" />
          </td>

          <td><input v-model="row.pa" @input="markTouched(row)" type="text" /></td>
          <td><input v-model="row.sc" @input="markTouched(row)" type="text" /></td>
          <td><input v-model="row.total" @input="markTouched(row)" type="text" /></td>
          <td><input v-model="row.pa2" @input="markTouched(row)" type="text" /></td>
          <td><input v-model="row.sc2" @input="markTouched(row)" type="text" /></td>
          <td><input v-model="row.total2" @input="markTouched(row)" type="text" /></td>
          <td><input v-model="row.newDue" @input="markTouched(row)" type="text" /></td>
          <td><input v-model="row.closingDue" @input="markTouched(row)" type="text" /></td>
          <td><input v-model="row.pa3" @input="markTouched(row)" type="text" /></td>
          <td><input v-model="row.sc3" @input="markTouched(row)" type="text" /></td>
          <td><input v-model="row.total3" @input="markTouched(row)" type="text" /></td>
          <td><input v-model="row.disbursedDate" @input="markTouched(row)" type="date" /></td>
          <td><input v-model="row.disbursedAmount" @input="markTouched(row)" type="text" /></td>
          <td><input v-model="row.gsPaBalance" @input="markTouched(row)" type="text" /></td>
          <td><input v-model="row.vsPaBalance" @input="markTouched(row)" type="text" /></td>
          <td class="view-td"><user-details-modal :member="row" /></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import userDetailsModal from './Modals/userDetailsModal.vue'

const props = defineProps({ data: Array })
const selectAll = ref(false)

const toggleAll = () => {
  props.data.forEach((r) => {
    r.selected = selectAll.value
    r.touched = true
  })
}
const markTouched = (r) => (r.touched = true)
</script>

<style scoped>
.table-container {
  max-height: 70vh;
  overflow: auto;
  border: 1px solid #ccc;
  border-radius: 6px;
  position: relative;
}

table {
  width: max-content;
  min-width: 100%;
  border-collapse: separate;
  border-spacing: 0;
  table-layout: fixed;
}

th,
td {
  border: 1px solid #ccc;
  padding: 6px 8px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  box-sizing: border-box;
  width: 100px;
}

thead th {
  background: #00cbfd;
  color: white;
  text-align: center;
  position: sticky;
  top: 0;
  z-index: 10;
}

.sticky-col {
  position: sticky;
  left: 0;
  background: #00cbfd;
  z-index: 11;
  color: white;
}

.sticky-col2 {
  position: sticky;
  left: 0;
  background: #00cbfd;
  z-index: 11;
  color: white;
}

.sticky-col2:nth-child(1) {
  left: 400px;
}

.sticky-col:nth-child(1) {
  left: 0px;
}
.sticky-col:nth-child(2) {
  left: 100px;
}
.sticky-col:nth-child(3) {
  left: 200px;
}
.sticky-col:nth-child(4) {
  left: 300px;
}
.sticky-col:nth-child(5) {
  left: 400px;
}
.sticky-col:nth-child(6) {
  left: 500px;
}
.sticky-col:nth-child(7) {
  left: 600px;
}
.sticky-col:nth-child(8) {
  left: 700px;
}
.sticky-col:nth-child(9) {
  left: 800px;
}
.sticky-col:nth-child(10) {
  left: 900px;
}

tbody .sticky-col {
  background: white;
  color: #000;
}

tbody {
  background: white;
  color: #000;
}

tr.edited td {
  background-color: #e2ffe2 !important;
}

input[type='text'] {
  width: 100%;
  border: none;
  background: white;
  outline: none;
}
input:focus {
  background: #eaf3ff;
}
input[type='checkbox'] {
  cursor: pointer;
}

.view-td {
  text-align: center;
  padding: 0;
}

tr.edited input[type='text'] {
  background-color: transparent !important;
}

tr.edited input[type='text']:focus {
  background-color: white !important;
}
</style>
