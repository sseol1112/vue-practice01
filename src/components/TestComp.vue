!<template>
    <h3>멤버 구성원 정보</h3>
    <ul class="members">
        <button @click="checkMemeber">멤버체크</button>
        <li v-for="i in member" :key="i">
            <h5>{{ i.number }}</h5>
            <p>{{ i.name }}</p>
            <p>{{ i.subject }}</p>
            <p>{{ i.level }}</p>
        </li>
    </ul>
    <div class="member-result"></div>
</template>

<script>
export default {
    name : 'test-component',
    data() {
        return {
            test : '',
            item : this.member
        } 
    },
    props : {
        member : Array
    },
    methods : {
        checkMemeber() {
            const result = document.querySelector(".member-result");
            const itemConvert = JSON.stringify(this.item);
            let html = '';
            html += '<br><strong>타이틀</strong>';
            html += '<div>' + itemConvert + '</div>';

            // result.append(itemConvert);
            result.insertAdjacentHTML('beforeend',html); // jQuery의 append()와 같은 역할
        }
    }
}
</script>

<style>
    .members {border:1px solid coral; padding:10px 20px;}
    .members li {display: flex; justify-content: space-between;}
</style>