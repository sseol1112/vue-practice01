<template>
    <div class="header">
        <ul class="gnb">
            <li v-for="menu in menus" :key="menu"><a href="">{{menu}}</a></li>
        </ul>
    </div>
    <div class="box_count">
        <div class="vmodel_box">
          <h3>v-model 테스트</h3>
          <ul>
            <li>
              <h4>1. input[type=text]</h4>
              <div class="text_type_wrap">
                <input v-model="textInput" placeholder="입력" />
                <p class="input_result">메세지 : {{ textInput }}</p>
              </div>
            </li>
            <li>
              <h4>2. input[type=checkbox]</h4>
              <div class="checkbox_wrap">
                <input type="checkbox" id="jack" value="Jack" v-model="checkedData">
                <label for="jack">Jack</label>
                <input type="checkbox" id="james" value="James" v-model="checkedData">
                <label for="james">James</label>
                <input type="checkbox" id="john" value="John" v-model="checkedData">
                <label for="john">John</label>
                <p class="input_result">체크한 이름 : {{ checkedData }}</p>
                <button @click="chkData">체크</button>
                <strong></strong>
              </div>
            </li>
            <li>
              <h4>3. input[type=radio]</h4>
              <div class="radio_wrap">
                <input type="radio" id="one" value="one" v-model="selectedNumber">
                <label for="one">One</label>
                <input type="radio" id="two" value="two" v-model="selectedNumber">
                <label for="two">Two</label>
                <p class="input_result">선택 넘버 : {{  selectedNumber }}</p>
              </div>
            </li>
          </ul>
        </div>
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
        <div class="builtIn_component_wrap">
          <h3>빌트인 컴포넌트 예제</h3>
          <ul>
            <li>
              <h4>1. transition</h4>
              <div class="transition_wrap">
                <button @click="show = !show">토글</button>
                <Transition>
                  <p v-if="show">안녕</p>
                </Transition>
              </div>
            </li>
          </ul>
        </div>
        <!-- test-component -->
        <TestComp :member="arrayVue"></TestComp>
    </div>
</template>

<script>
import ListItem from './components/ListItem.vue';
import CalcTemplate from './components/CalcTemplate.vue';
import TestComp from './components/TestComp.vue';

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
      menus : ['menu1','menu2','menu3','menu4','menu5'],
      textInput:'',
      checkedData:[],
      selectedNumber:'',
      show: ''
    }
  },
  components: {
    ListItem,
    CalcTemplate,
    TestComp
  },
  methods : {
    plus() {
      this.count += 1;
      console.log(this.count);

    },
    minus() {
      let countValue = this.count;
      if(countValue == 0 ){
        alert('0 이하로는 내릴 수 없습니다.');
        document.querySelector('.count_num').innerHTML = `<b style='color:#f00;'>${countValue}</b>`;
      } else {
        this.count -= 1;
        console.log(this.count);
      }
    },
    chkData() {
      let chkArray = this.checkedData;
      document.querySelector('.checkbox_wrap strong').innerText = chkArray;
      document.querySelector('.checkbox_wrap strong').style.color = "blue"
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

.header .gnb {
  display:flex; justify-content: space-around;
  li {
    background: skyblue; padding:10px 12px;
    a {
      color:#fff; 
    }
  }
}

@media screen and (max-width: 383px)  {
    .header .gnb li {border:1px solid #000; padding:10px 5px;}
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

.vmodel_box {
  h3 {
    border-bottom: 1px dashed #ccc;
    padding: 10px 0;
  }
  ul {
    li {
      border-bottom: 1px solid #ccc;
    }
  }
}
.input_result {
  font-weight: bold;
  color: darkcyan;
}


.builtIn_component_wrap {
  .v-enter-active,
  .v-leave-active {
    transition: opacity 1s ease;
  }

  .v-enter-from,
  .v-leave-to {
    opacity: 0;
  }
}
</style>
