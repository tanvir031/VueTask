<template>
  <div class="dropdown-container">
    <div class="dropdown-labels">
      <label
        ><p class="asterisk">*</p>
        <p class="labelName">Branch</p></label
      >
      <label
        ><p class="asterisk">*</p>
        <p class="labelName">Field Officer</p></label
      >

      <label
        ><p class="asterisk">*</p>
        <p class="labelName">Collection Type</p></label
      >

      <label
        ><p class="asterisk">*</p>
        <p class="labelName">Samity Day</p></label
      >

      <label
        ><p class="asterisk">*</p>
        <p class="labelName">Samity/Block/Group</p></label
      >
    </div>

    <div class="dropdownWithButton">
      <div class="dropdown-row">
        <select>
          <option v-for="item in branch">{{ item }}</option>
        </select>

        <select>
          <option v-for="item in fieldOfficer">{{ item }}</option>
        </select>
        <select>
          <option v-for="item in collectionType">{{ item }}</option>
        </select>
        <select>
          <option v-for="item in samityDay">{{ item }}</option>
        </select>
        <select>
          <option v-for="item in samity">{{ item }}</option>
        </select>
      </div>
      <button class="showDataBtn" @click="$emit('show-data')">Show Data</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const branch = ref(['Ragghunathpur', 'Kawran Bazar', 'Shamim Sharani'])
const fieldOfficer = ref(['Azim', 'alamin hossen', 'kawsar ali'])
const collectionType = ref(['exceptional collect'])
const samityDay = ref(['sunday', 'friday', 'saturday'])
const samity = ref(['211 shakrail'])
</script>

<style>
.dropdown-container {
  display: flex;
  flex-direction: column;
  align-items: start;
  gap: 8px;
  margin: 20px;
}

.dropdown-labels,
.dropdown-row {
  display: flex;
  justify-content: center;
  gap: 20px;
}

.dropdown-labels label {
  display: flex;
  width: 150px;
  margin-bottom: -15px;
  text-align: left;
  font-weight: 500;
}

.labelName {
  font-weight: normal;
}

.asterisk {
  color: red;
}

.dropdown-row select {
  width: 150px;
  padding: 6px;
  border-radius: 6px;
  border: 1px solid #ccc;
  background-color: white;
  transition:
    border-color 0.2s,
    box-shadow 0.2s;
}

.dropdownWithButton {
  display: flex;
  flex-direction: row;
}

.showDataBtn {
  background-color: #33d7fd; /* lighter cyan */
  color: black;
  border: 2px solid rgb(0, 247, 255);
  border-radius: 4px;
  padding: 8px 16px;
  font-weight: 500;
  cursor: pointer;
  transition:
    background-color 0.2s ease,
    transform 0.15s ease;
}

.showDataBtn:hover {
  background-color: #00cbfd;
  transform: translateY(-2px);
  box-shadow: 0 2px 6px rgba(0, 203, 253, 0.3);
}

.dropdown-row select:hover {
  border-color: #00bcd4;
  box-shadow: 0 0 6px rgba(0, 188, 212, 0.3);
}
</style>
