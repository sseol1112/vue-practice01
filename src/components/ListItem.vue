<template>
    <h2 v-html="introHtml"></h2>
    <h3>{{ introText }}</h3>
    <p v-text="infoText" style="color:#ccc;"></p>
    <ul class="info-list">
        <li v-for="itemKey in propItem" :key="itemKey"> 
            <div class="info-area">
                <span>{{ itemKey.number }}</span>
                <h3>{{ itemKey.name }}</h3>
                <p>{{ itemKey.subject }}</p>
                <h3>{{ itemKey.level }}</h3>
            </div>
        </li>
    </ul>
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
            console.log(user);
            user.append(this.userName.name);
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
</style>