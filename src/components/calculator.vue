<template>
  <div class="App">
    <div class="calculator">
      <div class="display">
        <span>{{calculatorValue || 0 }}</span>
      </div>
      <div class="operators" >
        <button v-for="number in operate" :key="number" @click="action(number)">{{number}}</button>
      </div>

      <div class="digits">
        <button v-for="number in digits" :key="number" @click="action(number)">{{ number }}</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return{
      calculatorValue: '',
      operate:['/', '*', '+', '-', '.', 'del', '='],
      digits: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0'],
      oparat: null,
      previousCalculatorValue: '',
    }
  },

  methods:{
    action(number){
      if (!isNaN(number) || number==='.'){
        this.calculatorValue += number + '';
      }

      if (number === 'del'){
        this.calculatorValue = '';
      }

      if (['/', '*', '+', '-', '.'].includes(number)){
          this.oparat = number;
          this.previousCalculatorValue = this.calculatorValue;
          this.calculatorValue = '';
      }

      if (number === '='){
        this.calculatorValue = eval(this.previousCalculatorValue + this.oparat + this.calculatorValue);
        this.previousCalculatorValue = '';
        this.oparat = null;
      }
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
:root{
  --primary: red;
  --secondary: blue;
  --dark: black;
  --light: white;
}
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans',sans-serif;
}
body{
  background-color: var(--light);
}
.App{
  display: flex;
  min-height: 100vh;
  align-items: center;
  justify-content: center;
  padding: 16px;
}
.calculator{
  width: 100%;
  max-width: 400px;
  background-color: aliceblue;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0px 2px 64px rgba(0, 0, 0, 0.2);
}

.display{
  padding: 16px;
  text-align: right;
  background-color: black;
  color: var(--light);
  font-size: 25px;
  font-weight: 300;
}
.display span{
  font-size: 14px;
  color: white;
}

button{
  appearance: none;
  border: none;
  outline: none;
  color: white;
  font-size: 15px;
  padding: 10px;
  cursor: pointer;
  transition: 0.7s;
}

button:hover{
  opacity: 0.4;
}

.operators{
  display: flex;
}
.operators button{
  flex: 1 1 0%;
  background-color: darkorange;
  font-weight: 700;
}

.digits{
  display: flex;
  flex-wrap: wrap;
}

.digits button{
  flex: 1 1 33.333%;
  max-width: 33.333%;
  background-color: black;
}
</style>
