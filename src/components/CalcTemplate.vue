<template>
  <div class="calcul_box">
        <div class="head_box">
            <h5>두 수를 입력 후 원하는 연산 버튼을 클릭해주세요.</h5>
            <button @click="resetFunc();" class="reset_btn">값 초기화</button>
        </div>        

        <button @click="calcFunc">+</button>
        <button @click="calcFunc">-</button>
        <button @click="calcFunc">*</button>
        <button @click="calcFunc">/</button>      

        <div class="form_box">
            <input type="number" name="num1" id="">
            <input type="number" name="num2" id="">
        </div>                      

        <div class="result_box">
            <h5>결과값</h5>
            <input type="text" class="result" name="result-value" value=""/>
        </div>
    </div>
</template>

<script>
export default {
    name : 'calculator-templates',
    data() {

    },
    props: {

    },
    methods : {
        calcFunc(e) {
            let num1 = parseInt(document.querySelector(".calcul_box .form_box input[name=num1]").value);
            let num2 = parseInt(document.querySelector(".calcul_box .form_box input[name=num2]").value);
            let num3 = '';
            let result = document.querySelector(".result_box .result");
            let typeVal = e.target.innerText;

            if((num1 != 0 && num2 != 0) && (!num1 || !num2)) {
                alert("계산할 값을 각각 입력해주세요.")                
            } else {
                switch(typeVal) {
                    case "+" :          
                        num3 = num1 + num2;
                        result.value = parseInt(num3);
                        break;
                    case "-" :
                        num3 = num1 - num2;
                        result.value = parseInt(num3);
                        break;
                    case "*" :
                        num3 = num1 * num2;
                        result.value = parseInt(num3);
                        break;
                    case "/" :
                        num3 = num1 / num2;
                        result.value = parseInt(num3);
                        break;
                    default :
                        alert("잘못된 계산식입니다. 내용을 확인해주세요.");
                }
            }
        },
        resetFunc() {
            let num1El = document.querySelector(".calcul_box .form_box input[name=num1]");
            let num2El = document.querySelector(".calcul_box .form_box input[name=num2]");
            let result = document.querySelector(".result_box .result");
        

            if(num1El.value.length > 0 || num2El.value.length > 0) {
                num1El.value = "";
                num2El.value = "";
                result.value = ""
                alert("값 초기화 완료");
            } else {
                alert("입력한 값이 없습니다.");
            }
        }
    }
}
</script>

<style lang="scss">

.calcul_box {
  border: 1px solid #222;
  margin: 10px 0;
  padding: 10px;
  .head_box {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 12px;
    h5 {
        font-size: 16px;
        line-height: 21px;
        margin: 0 5px;
    }
    button {
        background:#fff;
        color: #222;
        border: 1px solid #222;
    }
  }
  .form_box {
    display: flex;  
    margin-top: 20px;
    input {
      width:calc(50% - 10px);
      margin: 0 5px;
      text-align: center;
    }
  }
  .result_box {
    h5 {
        margin: 10px 0;
    }
    input {
        text-align: center;
    }
  }
}
</style>