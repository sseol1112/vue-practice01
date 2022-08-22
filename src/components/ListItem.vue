<template>
    <h1>{{ introText }}</h1>
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
    name : 'powder-compon',
    data() {
        return {
            'introText' : '사용자 정보 리스트 입니다.',
            'propItem' : this.testProp,
            'infoText' : 'components와 props로 부모데이터로 받아온 배열 임의의 propItem 변수에 담아 데이터 출력되도록 활용하였음.'
        }
    },
    props : {
        testProp : Array
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