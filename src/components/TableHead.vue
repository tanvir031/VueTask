<template>
  <div class="tablehead">
    <p>Total Member: {{ props.data.length }}</p>
    <p>Loan Recoverable: {{ calcLoanRecoverable() }}</p>
    <p>Total Collection: {{ calcTotalCollection() }}</p>
    <p>Loan: {{ calcLoan() }}</p>
    <p>GS: {{ calcGS() }}</p>
    <p>VS: {{ calcVS() }}</p>
    <p>DPS: {{ calcDPS() }}</p>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
  data: {
    type: Array,
    required: true,
  },
})

const calcLoanRecoverable = () => {
  let LoanRecoverable = 0
  props.data.map((item) => {
    const lnRecoverFloat = parseFloat(item.total2)
    if (!Number.isNaN(lnRecoverFloat)) LoanRecoverable += lnRecoverFloat
  })

  return LoanRecoverable
}

const calcTotalCollection = () => {
  let totalCollection = 0

  props.data.map((item) => {
    const collectionFloat = parseFloat(item.total)
    if (!Number.isNaN(collectionFloat)) totalCollection += collectionFloat
  })

  return totalCollection
}

const calcLoan = () => {
  let Loan = 0
  props.data.map((item) => {
    const LoanFloat = parseFloat(item.loan)
    if (!Number.isNaN(LoanFloat)) Loan += LoanFloat
  })

  return Loan
}

const calcGS = () => {
  let GS = 0
  props.data.map((item) => {
    const GSFloat = parseFloat(item.gs)
    if (!Number.isNaN(GSFloat)) GS += GSFloat
  })
  return GS
}

const calcVS = () => {
  let VS = 0
  props.data.map((item) => {
    const VSFloat = parseFloat(item.vs)
    if (!Number.isNaN(VSFloat)) VS += VSFloat
  })

  return VS
}

const calcDPS = () => {
  let DPS = 0
  props.data.map((item) => {
    const DPSFloat = parseFloat(item.dps)
    if (!Number.isNaN(DPSFloat)) DPS += DPSFloat
  })

  return DPS
}
</script>

<style>
.tablehead {
  background-color: transparent;
  display: flex;
  justify-content: space-between;
  padding: 10px;
  margin-left: 50px;
  margin-right: 50px;
  gap: 20px;
  flex-direction: row;
}

p {
  font-weight: bold;
}
</style>
