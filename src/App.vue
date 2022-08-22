<template>
    <div class="header">
        <ul>
            <li v-for="menu in menus" :key="menu"><a href="#">{{menu}}</a></li>
        </ul>
    </div>
    <div class="box_count">
        
        <h1><strong>*</strong> count Number 체크!</h1>
        <h1>{{ count }}</h1>
        <button @click="plzus">+ </button>
        <button @click="minus">-</button>

        <!-- component 사용 -->
        <ListItem :testProp="arrayVue"></ListItem>

        <!-- 이미지 -->
        <!-- <div class="img_wrap">
          <img src="./assets/logo.png" />
        </div> -->

    </div> 
</template>

<script>
import ListItem from './components/ListItem.vue';

export default {
  name: 'App',
  data() {
    return {
      count : 0,
      name : 'greek',
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
      }],
      menus : ['menu1','menu2','menu3','menu4','menu5'],
    }
  },
  components: {
    ListItem
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
      } else {
        this.count -= 1;
        console.log(this.count);
      }
    }

  }  
}

</script>

<style>
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

.header ul {display:flex; justify-content: space-around;}
.header ul li {padding:10px 12px; background: skyblue;}
.header ul li a{ color:#fff;}

@media screen and (max-width: 383px)  {
    .header ul li {border:1px solid #000; padding:10px 5px;}
}
</style>
