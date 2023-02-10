<template>
  <section class="calculator">
    <div class="calculator-container">
        <div class="calculator_body">
          <div class="calculator_body_answer">
            <div class="answer_history">{{history}}</div>
            <div class="answer_value">{{answer}}</div>
          </div>
          <div class="calculator_body_keys">
            <div class="body_key" v-for="key in keys" :key="key" @click="addAnswer(key)">{{ key }}</div>
          </div>
        </div>
    </div>
  </section>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      keys: ['C', '<=', '%', '/', '7', '8', '9', '*', '4', '5', '6', '-', '1', '2', '3', '+', '00', '0', ',', '='],
      answer : '',
      history: null
    }
  },
  methods: {
    addAnswer(num){
      if(num == '='){
        this.answerValue()
      }else if(num == 'C'){
        this.answer = ''
        this.history = ''
      }else if(num == '<='){
        this.answer = this.answer.slice(0, -1)
      }else if(num == ','){
        this.answer += '.'
      }else{
        this.answer += num
      }
    },  
    answerValue(){
      this.history = this.answer;
      let answers = eval(this.answer)
      const f = x => ( (x.toString().includes('.')) ? (x.toString().split('.').pop().length) : (0) );
      this.answer = f(answers)
      if(f(answers) == 0){
        this.answer = answers
      }else{
        this.answer = answers.toFixed(2)
      }
    }
  }
}
</script>

<style>
*{
  box-sizing: border-box;
}
body{
  margin: 0;padding: 0;
}
.calculator {
  color: #fff;
  height: 101vh;
  background: #FF8484;
  padding: 40px 0;
}
.calculator-container {
  background: #f39b9b;
  padding: 35px;
  border-radius: 18px;
  backdrop-filter: blur(2px);
  max-width: 616px;
  margin: 0 auto;
}
.calculator_body {
  font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
  margin: 0 auto;
  border-radius: 18px;
  padding: 15px 50px;
  /* box-shadow: 0px 82px 158px rgba(0, 0, 0, 0.3), 0px 24.7206px 47.6324px rgba(0, 0, 0, 0.2), 0px 10.2677px 19.7841px rgba(0, 0, 0, 0.1), 0px 3.71362px 7.1555px rgba(0, 0, 0, 0.1); */
  /* width: 554px; */
  background: linear-gradient(155.23deg, #28518E 0%, #3A77D1 100%);
}
.calculator_body_answer {
  text-align: right;
  border-bottom: 2px solid #fff;
  /* transition: all .3s ease; */
}
/* .calculator_body_answer::before{
  cont
} */
.answer_history {
  padding: 90px 0 0 0;
  font-size: 24px;
  margin-bottom: 30px;
}
.answer_value {
  font-size: 56px;
  margin-bottom: 20px;
  transition: all .3s ease;
}
.calculator_body_keys {
  display: flex;
  justify-content: space-between;
  font-size: 30px;
  flex-wrap: wrap;
  margin-top: 35px;
  color: #fff;
}
.body_key{
  cursor: pointer;
  margin-bottom: 14px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 100px;
  border-radius: 50%;
  transition: all .3s ease;
}
.body_key:hover{
  background: #ffffff2a;
  color: #f2f2f2;
}
.body_key:last-child{
  color: #2B589A;
  background: #fff;
}
.body_key:last-child:hover{
  background:rgb(192, 192, 192);
}
</style>
