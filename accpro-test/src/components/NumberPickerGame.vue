<template>
  <div class="hello">
      <h1>Number Picker Game</h1>
      <p>Pick 8 unique numbers from 1 to 80:</p>
      <div>
        <input type="number" v-model="pickedNumbers[index]" min="1" max="80" v-for="(number, index) in 8" :key="index">
      </div>
      <br>
      <button @click="submitNumbers">Submit</button>
      <br><br>
      <p>Randomly drawn numbers:</p>
      <div>{{ drawnNumbers.join(', ') }}</div>
      <br>
      <p>Your winnings: {{ totalWinning }}</p>
  </div>
</template>

<script>
export default {
  name: 'NumberPickerGame',
  data() {
    return {
      pickedNumbers: [],
      drawnNumbers: [],
      totalWinning: 0
    }
  },
  methods: {
    submitNumbers() {
      if (this.verifyPickedNumberLength() === false) {
        alert('Please pick 8 unique numbers!');
        return false;
      }

      if (this.verifyNegativeNumber() === false) {
        alert('Please use positive numbers!');
        return false;
      }

      this.drawnNumbers = [];
      for (let i = 0; i < 20; i++) {
        const randomNum = Math.floor(Math.random() * 80) + 1;
        this.drawnNumbers.push(randomNum);
      }
      this.calculateWinnings();
    },
    verifyPickedNumberLength() {
      if (this.pickedNumbers.length < 8){
        return false;
      }

      return true;
    },
    verifyNegativeNumber() {
        let negativeList = this.pickedNumbers.filter((number) => {
            return number < 1;
        });

        if (negativeList.length > 0) {
          return false;
        }

        return true;
    },
    resetForm() {
      this.drawnNumbers = [];
      this.totalWinning = 0;
    },
    calculateWinnings() {
      const hits = this.getHits();
      let pay = 0;

      switch (hits) {
        case 8:
          pay = 10000;
          break;
        case 7:
          pay = 1650;
          break;
        case 6:
          pay = 100;
          break;
        case 5:
          pay = 12;
          break;
        case 4:
          pay = 2;
          break;
        case 3:
        case 2:
        case 1:
          pay = 0;
          break;
      }

      if (this.drawnNumbers.length > 0 && this.pickedNumbers.includes(this.drawnNumbers[19])) {
        pay *= 2;
      }

      this.totalWinning = pay;
    },
    getHits() {
      let hits = 0;
      for (const number of this.pickedNumbers) {
        if (this.drawnNumbers.includes(number)) {
          hits++;
        }
      }
      return hits;
    }
  }
}
</script>

