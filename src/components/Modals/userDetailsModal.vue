<template>
  <div>
    <EyeButton class="view-btn" @click="openModal" title="View Details" />

    <div v-if="isOpen" class="modal-overlay" @click.self="closeModal">
      <div class="modal-header">
        <p class="header-name">Member Information</p>
        <Icon icon="ph:x-bold" class="close-btn" @click="closeModal" />
      </div>
      <div class="modal-content">
        <div class="card-1" v-if="user">
          <div class="table personal-details-table">
            <div class="table-row" v-for="(value, label) in personalDetails" :key="label">
              <div class="table-cell label">{{ label }}</div>
              <div class="table-cell value">{{ value }}</div>
            </div>
          </div>
          <div class="photo">
            <img :src="user.personalDetails.photo || defaultPhoto" alt="User Photo" />
          </div>
        </div>

        <div class="card-2" v-if="user">
          <div class="bank-details-header">
            <p>Savings Information</p>
          </div>

          <div class="table bank-details-table">
            <div class="table-row" v-for="(value, label) in bankDetails" :key="label">
              <div class="table-cell label">{{ label }}</div>
              <div class="table-cell value">{{ value }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import EyeButton from '../Buttons/eyeButton.vue'
import { inject } from 'vue'
import { Icon } from '@iconify/vue'

const users = inject('users')
const defaultPhoto = '../../../public/placeholderimage.png'

const props = defineProps({
  memberId: String,
})

const isOpen = ref(false)
const user = ref(null)

const openModal = () => {
  user.value = users.value.find((u) => u.userId === props.memberId)
  isOpen.value = true
}

const closeModal = () => (isOpen.value = false)

const personalDetails = computed(() => {
  if (!user.value) return {}
  return {
    Name: `${user.value.personalDetails.firstName} ${user.value.personalDetails.lastName}`,
    Phone: user.value.personalDetails.mobileNo,
    Email: user.value.personalDetails.email,
    Guardian: user.value.personalDetails.guardianName,
  }
})

const bankDetails = computed(() => {
  if (!user.value) return {}
  return {
    'Account No': user.value.bankLoanDetails.accountNumber,
    'Account Opening Date': user.value.bankLoanDetails.accountOpeningDate,
    'Loan Type': user.value.bankLoanDetails.loanType,
    'Loan Amount': user.value.bankLoanDetails.loanAmount,
    'Principal Balance': user.value.bankLoanDetails.principalBalance,
    'Installment Size': user.value.bankLoanDetails.installmentSize,
    'Interest Rate': `${user.value.bankLoanDetails.interestRate}%`,
    'Loan Status': user.value.bankLoanDetails.loanStatus,
    'Samity Day / Block / Group': `${user.value.samityDetails.samityDay} / ${user.value.samityDetails.samityBlock} / ${user.value.samityDetails.samityGroup}`,
    'Software ID': user.value.employmentDetails.softwareId,
  }
})
</script>

<style scoped>
.view-btn {
  border: none;
  background: transparent;
  cursor: pointer;
  padding: 2px;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  padding-top: 20px;
  z-index: 1000;
  overflow-y: auto;
}

.modal-content {
  background: white;
  padding: 20px;
  border-bottom: 6px;
  width: 60vw;
  min-width: 400px;
  max-width: 90vw;
  max-height: 90vh;
  overflow-y: auto;
}

.card-1 {
  display: flex;
  background: #ebebeb;
  padding: 30px;
  border-radius: 6px;
  margin-bottom: 15px;
}

.card-2 {
  display: flex;
  background: #ebebeb;
  padding-left: 30px;
  padding-right: 30px;
  flex-direction: column;
  border-radius: 6px;
  margin-bottom: 15px;
}

.table {
  display: table;
  width: 100%;
  border-collapse: collapse;
  background: white;
}

.table-row {
  display: table-row;
}

.table-cell {
  display: table-cell;
  padding: 8px 12px;
  border: 1px solid #ccc;
}

.table-row:hover .table-cell {
  background: #d0ebff;
}

.label {
  font-weight: 500;
  text-align: left;
  width: 50%;
}

.value {
  text-align: left;
  width: 50%;
}

.photo {
  display: flex;
  align-items: center;
  padding-left: 30px;
}

.photo img {
  width: 100px;
  height: 100px;
  object-fit: cover;
}

.close-btn {
  width: 30px;
  height: 30px;
  color: rgba(0, 0, 0, 0.5);
  cursor: pointer;
}

.close-btn:hover {
  scale: 1.2;
  color: rgba(0, 0, 0, 0.8);
  transition: 0.3s ease;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  width: 60vw;
  text-align: center;
  align-items: center;
  background-color: rgb(0, 153, 255);
  padding-left: 20px;
  padding-right: 20px;
  border-top-left-radius: 6px;
  border-top-right-radius: 6px;
  text-shadow: 1px 1px 1px rgba(0, 0, 0, 0.1);
}

.header-name {
  text-align: start;
  font-size: larger;
  color: white;
}

.bank-details-header {
  width: calc(100% + 60px);
  margin-left: -30px;
  margin-right: -30px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.2);
  padding: 8px 30px;
  box-sizing: border-box;
}

.bank-details-header p {
  text-align: start;
  font-size: x-large;
  font-weight: bold;
  padding: 10px;
  margin: 0;
  align-items: center;
}

.bank-details-table {
  margin-top: 25px;
}
</style>
