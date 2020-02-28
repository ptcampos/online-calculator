<template>
  <q-page class="bg-secondary column flex flex-center">
    <div class="text-h3 text-white">Online Calculator</div>
    <q-card class="q-mt-md my-card">
      <q-card-section class="row q-col-gutter-md">
        <div class="col-xs-2">
          <CalcButton @onClick="evt => onClick(evt, 'c')" label="C" bgColor="orange" />
        </div>
        <div class="col-xs-10">
          <div
            :style="{
              display: 'flex',
              flexDirection: 'row',
              justifyContent: 'flex-end',
              alignItems: 'center',
              height: '100%',
              fontWeight: 'bold',
              fontSize: '1.5em'
            }"
          >
            {{ resultDisplay }}
          </div>
        </div>
        <div
          class="col-xs-3"
          :key="n"
          v-for="n in [7, 8, 9, '+', 4, 5, 6, '-', 1, 2, 3, '*', 0, '.', '=', '/']"
        >
          <CalcButton
            @onClick="evt => onClick(evt, n)"
            :label="n"
            :bgColor="n === '=' ? 'negative' : 'primary'"
          />
        </div>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
import CalcButton from 'components/CalcButton'

export default {
  name: 'PageIndex',

  data() {
    return {
      resultDisplay: '0',
      num1: null,
      num2: null,
      operation: '',
      switch: false
    }
  },

  components: {
    CalcButton
  },

  methods: {
    stopPropagation(event) {
      event.stopPropagation()
      event.preventDefault()
    },
    sum(a, b) {
      return a + b
    },
    divide(a, b) {
      return a / b
    },
    subtract(a, b) {
      return a - b
    },
    multiplies(a, b) {
      return a * b
    },
    isOnFirstNumber() {
      return this.operation === ''
    },
    handleNumberClick(n) {
      if ((this.isOnFirstNumber() && this.resultDisplay === '0') || this.switch) {
        this.resultDisplay = n
        this.switch = false
        return
      }
      this.resultDisplay = `${this.resultDisplay}${n}`
    },
    handleClearClick() {
      this.resultDisplay = '0'
      this.num1 = null
      this.num2 = null
      this.operation = ''
    },
    handleDotClick() {
      if (this.resultDisplay.indexOf('.') > -1) {
        return
      }
      this.resultDisplay = `${this.resultDisplay}.`
    },
    handleOperationClick(operation) {
      this.operation = operation
      this.num1 = parseFloat(this.resultDisplay)
      this.switch = true
    },
    getAndShowResult() {
      const lastInsert = parseFloat(this.resultDisplay)
      switch (this.operation) {
        case '+':
          this.resultDisplay = this.sum(this.num1, parseFloat(this.resultDisplay))
          break
        case '-':
          this.resultDisplay = this.subtract(this.num1, parseFloat(this.resultDisplay))
          break
        case '/':
          this.resultDisplay = this.divide(this.num1, parseFloat(this.resultDisplay))
          break
        case '*':
          this.resultDisplay = this.multiplies(this.num1, parseFloat(this.resultDisplay))
          break
      }
      this.num1 = lastInsert
    },
    onClick(event, n) {
      this.stopPropagation(event)

      const insert = parseInt(n, 10)

      if (!isNaN(insert)) {
        this.handleNumberClick(n)
        return
      }
      if (String(n).toLowerCase() === 'c') {
        this.handleClearClick()
      } else if (String(n).toLowerCase() === '.') {
        this.handleDotClick()
      } else if (String(n).toLowerCase() === '=') {
        this.getAndShowResult()
      } else {
        this.handleOperationClick(n)
      }
    }
  }
}
</script>

<style scoped lang="scss">
.my-card {
  width: 400px;
  max-width: 80%;
}
</style>
