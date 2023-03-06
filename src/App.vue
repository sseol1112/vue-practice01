<template>
    <div class="header">
        <ul>
            <li v-for="menu in menus" :key="menu"><a href="#">{{menu}}</a></li>
        </ul>
    </div>
    <div class="box_count">
        
        <h1><strong>*</strong> count Number 체크!</h1>
        <p class="blind">테스트 웹표준 blind 처리</p>
        <h2 class="count_num">{{ count }}</h2>
        <button @click="plus">+</button>
        <button @click="minus">-</button>

        <CalcTemplate ></CalcTemplate>

        <!-- component 사용 -->
        <ListItem :testProp="arrayVue" :user="userInfo"></ListItem>

        <!-- 이미지 -->
        <!-- <div class="img_wrap">
          <img src="./assets/logo.png" />
        </div> -->

    </div> 
</template>

<script>
import ListItem from './components/ListItem.vue';
import CalcTemplate from './components/CalcTemplate.vue';

export default {
  name: 'App',
  data() {
    return {
      count : 0,
      name : 'greek',
      userInfo : {
        'name' : 'guest1',
        'grade' : 'supervisor'
      },
      arrayVue : [{
        'number' : '1',
        'name' : 'john',
        'subject' : 'math',
        'level':'10'
      },{
        'number' : '2',
        'name' : 'tom',
        'subject' : 'english',
        'level':'5'
      },{
        'number' : '3',
        'name' : 'amy',
        'subject' : 'english',
        'level':'3'
      },{
        'number' : '4',
        'name' : 'testboy',
        'subject' : 'korean',
        'level' : '2'
      }],
      menus : ['menu1','menu2','menu3','menu4','menu5']
    }
  },
  components: {
    ListItem,
    CalcTemplate
  },
  methods : {
    plus() {
      this.count += 1;
      console.log(this.count);

    },
    minus() {
      let countValue = this.count;
      //let testA = document.querySelector('.count_num');
      if(countValue == 0 ){
        alert('0 이하로는 내릴 수 없습니다.');
        document.querySelector('.count_num').innerHTML = `<b style='color:#f00;'>${countValue}</b>`;
      } else {
        this.count -= 1;
        console.log(this.count);
      }
    },
    calcFunc(e) {
      let num1 = parseInt(document.querySelector(".calcul_box .form_box input[name=num1]").value);
      let num2 = parseInt(document.querySelector(".calcul_box .form_box input[name=num2]").value);
      let num3 = '';
      let result = document.querySelector(".result_box h5 .num");
      let typeVal = e.target.innerText;

    
      switch(typeVal) {
        case "+" :          
          num3 = num1 + num2;
          result.innerHTML = parseInt(num3);
          break;
        case "-" :
          num3 = num1 - num2;
          result.innerHTML = parseInt(num3);
          break;
        case "*" :
          num3 = num1 * num2;
          result.innerHTML = parseInt(num3);
          break;
        case "/" :
          num3 = num1 / num2;
          result.innerHTML = parseInt(num3);
          break;
        default :
          alert("잘못된 계산식입니다. 내용을 확인해주세요.");
      }
      
    }

  }  
}

</script>

<style lang="scss">

/* common.css */
//폰트 컬러
.fc-blue {color: #00f;}
.blind {position: absolute;overflow: hidden; width: 1px; height: 1px; margin: -1px; clip:rect(0,0,0,0);}
ul { list-style: none; padding:0; }
a {text-decoration: 0; color: #2c3e50;}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  max-width: 550px;
  margin:0 auto;
}

.header ul {
  display:flex; justify-content: space-around;
  li {
    background: skyblue; padding:10px 12px;
    a {
      color:#fff; 
    }
  }
}

@media screen and (max-width: 383px)  {
    .header ul li {border:1px solid #000; padding:10px 5px;}
}

.calcul_box {
  
  .form_box {
    display: flex;  
    margin-top: 20px;
    input {
      width:calc(50% - 10px);
      margin: 0 5px;
    }
  }
}
.box_count  {
  button {
  margin: 0 5px;
  background: #2c3e50;
  color: #fff;
  border: 0;
  padding:12px 18px;
  border-radius: 10px;
  font-size: 16px;
  cursor: pointer;
  }
}

</style>
