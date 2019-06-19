<template>
  <div>
    <h1>Calculator with Vue.js</h1>
    <div class="calc">
      <input class="small-text" type="text" v-model="inpText">
      <input type="text" v-model="inpText2"  maxlength="11" size="11">
      <div class="calc-content">
        <span @click="func2('%')">%</span>
        <span @click="func2('√')">√</span>
        <span @click="func2('2')">х&sup2;</span>
        <span @click="func2('/')">1⁄ х</span><br>
        <span @click="remove()">CE</span>
        <span @click="removeAll()">C</span>
        <span @click="del()">x</span>
        <span @click="func('/')">&divide;</span><br> <!-- бөлу -->
        <span class="nmbr" @click="number(7)">7</span>
        <span class="nmbr" @click="number(8)">8</span>
        <span class="nmbr" @click="number(9)">9</span>
        <span @click="func('*')">&times;</span><br> <!-- көбейту -->
        <span class="nmbr" @click="number(4)">4</span>
        <span class="nmbr" @click="number(5)">5</span>
        <span class="nmbr" @click="number(6)">6</span>
        <span @click="func('-')">-</span><br> <!-- алу -->
        <span class="nmbr" @click="number(1)">1</span>
        <span class="nmbr" @click="number(2)">2</span>
        <span class="nmbr" @click="number(3)">3</span>
        <span @click="func('+')">+</span><br> <!-- қосу -->
        <span @click="func('+-')">±</span>
        <span class="nmbr" @click="number(0)">0</span>
        <span @click="number('.')">,</span>
        <span @click="value()" @keyup.enter="value()">=</span><br>
      </div>

    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        inpText: '',
        inpText2: '',
        counter1: 0,
        counter2: 0,
        qw: false,
        zx: false,
        val: 0,
        mark: '',
        count: 0
      }
    },
    methods: {
      number(e) { 
        if(this.zx){
          this.inpText2 = ''
          this.zx = false;
        }
        this.count++;
        if(this.inpText2 === '') { this.count = 0 }
        if(this.count > 8){
          this.inpText2 = this.inpText2
        }
        else{
          this.inpText2 += e;
        }
      },
      del(){
        this.inpText2 = this.inpText2.slice(0,-1)
      },
      remove(){
        this.inpText2 = ''
      },
      removeAll(){
        this.inpText2 = this.inpText = '',
        this.counter1 = this.counter2 = 0
      },
      func(e){
        this.inpText = this.counter1 =  this.inpText2;
        this.inpText += ' ' + e;
        this.counter1 = parseFloat(this.counter1);
        if(e === '+-'){
          this.inpText = ''
          this.inpText2 = -this.inpText2
        }
        else{
          this.inpText2 = ''
        }
        this.qw = true;
        this.mark = e
        // this.count = 0
      },
      func2(e){
        switch(e){
          case '%':
            this.inpText = '%(' +this.inpText2 + ')'
            this.val = this.inpText2 / 100;
            break;
          case '√':
            this.inpText = '√(' + this.inpText2 + ')'
            this.val = Math.sqrt(this.inpText2);            
            break;
          case '/':
            this.inpText = '1/(' +this.inpText2 + ')'
            this.val = 1.0 / parseFloat(this.inpText2)
            break;
          case '2':
            this.inpText = 'sqr(' + this.inpText2 + ')'
            this.val = this.inpText2 * this.inpText2;
            break;
        }
        this.inpText2 = this.val;  + ''
        this.zx = true;
        // this.count = 0
      },
      value(){
        if(this.qw){
          this.counter2 = parseFloat(this.inpText2);
          switch(this.mark){
            case '+':
              this.val = this.counter1 + this.counter2;
              break;
            case '-':
              this.val = this.counter1 - this.counter2;
              break;
            case '/':
              this.val = this.counter1 / this.counter2;
              break;
            case '*':
              this.val = this.counter1 * this.counter2;
              break;
          }
        }
        else{
          this.val = this.inpText2
        }
        if(this.val>99999999999) {
          this.val = this.val.toPrecision(8)
        }
        this.inpText2 = this.val; 
        console.log(this.val)
        this.inpText = ''
        this.zx = true;
      }
    },
  }
</script>

<style scoped>
  .calc{
    width: 320px;
    background: #787575;
    margin: 0 auto;
    padding-top: 1%;
    color: #fff;
    padding-bottom: 3px;
  }
  .calc .small-text{
    font-size: 14px;
  }
  .calc input{
    width: 95%;
    border: none;
    background: #787575;
    color: #fff;
    text-align: right;
    font-weight: bolder;
    font-size: 42px;
    outline: none;
  }
  .calc-content{
    width: 98%;
    margin: 0 auto;
    display: flex;
    flex-wrap: wrap;
  }
  span{
    background: #3f3f3f;
    margin: 1px;
    flex: 23%;
    height: 45px;
    font-size: 20px;
    line-height: 40px;
  }
  .nmbr{
    background: #151515;
    font-weight: bolder;
    font-size: 22px;
    line-height: 42px;
  }
</style>