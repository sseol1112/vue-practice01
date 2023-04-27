<template>
    <h2 v-html="introHtml"></h2>
    <h3>{{ introText }}</h3>
    <p v-text="infoText" style="color:#ccc;"></p>
    <ul class="info-list">
        <li v-for="itemKey in propItem" :key="itemKey"> 
            <div class="info-area">
                <span>{{ itemKey.number }}</span>
                <h3 class="name">{{ itemKey.name }}</h3>
                <p class="subject">{{ itemKey.subject }}</p>
                <h3 class="level">{{ itemKey.level }}</h3>
                <input type="radio" value="" name="check"/>
            </div>
        </li>
    </ul>
    <div class="btn-wrap">
        <button class="btn" id="submit" @click="submitSelected">제출</button>
        <button class="btn" id="getter" @click="getSelectedResult">제출한 내용 확인하기</button>
    </div>
    <Transition>
        <div class="getter-result">
            <p class="result"></p>
        </div>
    </Transition>
</template>

<script>

export default {
    name : 'powder-component',
    data() {
        return {
            'introText' : '사용자 정보 리스트 입니다.',
            'propItem' : this.testProp,
            'userName' : this.user,
            'infoText' : 'components와 props로 부모데이터로 받아온 배열 임의의 propItem 변수에 담아 데이터 출력되도록 활용하였음.',
            'introHtml' : '<p>안녕하세요! <span class="fc-blue username"></span>님 반갑습니다</p>'
        }
    },
    props : {
        testProp : Array,
        user : Object
    },
    methods : {
        userCheck() {
            let user = document.querySelector('.username');
            user.append(this.userName.name);
        },
        submitSelected() {
            let selectedList =document.querySelector('.info-area input[type=radio]:checked').closest('li');
            let selectedNum = selectedList.querySelector('span').innerText;
            let selectedName = selectedList.querySelector('.name').innerText;
            let selectedSubject = selectedList.querySelector('.subject').innerText;
            let selectedLevel = selectedList.querySelector('.level').innerText;


            if(selectedList === null || selectedList === "" || selectedList === undefined) {
                alert('선택한 값이 없습니다.');
            } else {
                let selectedResult = [selectedNum,selectedName,selectedSubject,selectedLevel];
                let resultValue = JSON.stringify(selectedResult);
                
                console.log(resultValue);
                sessionStorage.setItem('selectedResult', resultValue);
                //localStorage -> sessionStorage로 변경!
                //localStorage : 브라우저 종료해도 저장값 남아있음 but, sessionStorage는 브라우저를 종료하면 데이터도 삭제됨!
            }

        },
        getSelectedResult() {
            let result = document.querySelector('.getter-result .result');
            let data = JSON.parse(sessionStorage.getItem('selectedResult'));
            console.log(data);
            if(data != null && data != "") {
                result.innerHTML = (`<div>
                                        <ul class="info-list">
                                            <li v-for="itemKey in propItem" :key="itemKey"> 
                                                <div class="info-area">
                                                    <span>${data[0]}</span>
                                                    <h3 class="name">${data[1]}</h3>
                                                    <p class="subject">${data[2]}</p>
                                                    <h3 class="level">${data[3]}</h3>
                                                </div>
                                            </li>
                                        </ul>
                                    </div>`);
            } else {
                alert("저장된 데이터가 없습니다.");
            }
        }
    },
    mounted() {
        this.userCheck();

    }
}
</script>

<style>
    .info-list {
        max-width:350px;
        margin:0 auto;
        border-top:1px solid #ccc;
    }
    .info-list li{
        border-bottom:1px solid #ccc;
    }
    .info-area {
        display: flex;
        justify-content: space-between;
        align-items:center;
    }
    .info-area h3 {
        flex-grow: 1;
    }
    .btn-wrap {
        margin:15px 0;
    }
</style>