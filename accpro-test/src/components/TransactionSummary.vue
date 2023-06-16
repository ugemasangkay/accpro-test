<template>
  <div>
    <h2>Transaction Summary</h2>
    <div>
      <label for="depositAmount">Deposit Amount:</label>
      <input type="number" id="depositAmount" v-model="depositAmount" />
    </div>
    <button class="btn-submit" @click="calculateBonus">Submit</button>
    <div v-if="transactionSummary">
      <p>Deposit Amount: $ {{ transactionSummary.depositAmount.toFixed(2) }}</p>
      <p>Bonus Amount: $ {{ transactionSummary.bonusAmount.toFixed(2) }}</p>
      <p>Total Amount: $ {{ transactionSummary.totalAmount.toFixed(2) }}</p>
    </div>
  </div>
</template>

<script>
import promoSettings from './promoSettings.json';

export default {
  name: 'TransactionSummary',
  data() {
    return {
      depositAmount: 0,
      transactionSummary: null,
    };
  },
  methods: {
    calculateBonus() {
      const bonusMatrix = promoSettings.bonus_matrix;
      let bonusAmount = 0;

      for (const level of bonusMatrix) {
        if (this.depositAmount >= level.min_amount) {
          if (level.bonus_type === 'F') {
            bonusAmount = Math.min(level.bonus_value, promoSettings.max_bonus_amount);
          } else if (level.bonus_type === 'P') {
            bonusAmount = Math.min(this.depositAmount * level.bonus_value, promoSettings.max_bonus_amount);
          }
        }
      }

      const totalAmount = this.depositAmount + bonusAmount;
      this.transactionSummary = {
        depositAmount: this.depositAmount,
        bonusAmount,
        totalAmount,
      };
    },
  },
};
</script>

<style scoped>
.btn-submit {
  margin-top: 2%;
}
</style>