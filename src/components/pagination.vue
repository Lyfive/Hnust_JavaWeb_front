
<script>
export default {
    data() {
        return {
            page: 1, // 当前页码
            pageMax: 5, // 最大页数
        }
    },
    methods: {
        ischeck(num) {
            if (num == this.page) {
                return "check";
            }
        },
        change(aList) {
            this.page = aList;
            this.sendPage();
        },
        sendPage(){
            this.$emit('getPage',this.page);
        }
    },
    computed: {
        pageList() {
            return [1, 2, 3, 4, 5] // 页码列表
        }
    }
};
</script>
<template>
    <div class="page">
        <span>
            <img src="../assets/up-page.png" alt style="width:1.25rem;" />
        </span>
        <span
            v-for="aList in pageList"
            v-bind:key="aList"
            :class="{ check: ischeck(aList) }"
            @click="change(aList)"
        >{{ aList }}</span>
        <span>
            <img src="../assets/down-page.png" alt style="width:1.25rem;" />
        </span>
        <div class="explain">4条/页</div>
        <span>跳至</span>
        <div class="explain">
            <input type="text" id="jump" maxlength="3" />
        </div>
        <span>页</span>
    </div>
</template>
<style scoped>
.page {
    position: relative;
    height: 2rem;
}

.page span {
    position: relative;
    display: inline-block;
    margin-left: 0.75rem;
    font-size: 1rem;
    width: 1.25rem;
    height: 2rem;
    line-height: 2rem;
    text-align: center;
    vertical-align: top;
    white-space: nowrap;
}
.page span img {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
.explain {
    position: relative;
    top: 50%;
    transform: translateY(-50%);
    display: inline-block;
    height: 1.25rem;
    font-size: 0.9rem;
    padding-left: 0.25rem;
    padding-right: 0.25rem;
    margin-left: 1rem;
    line-height: 1.25rem;
    letter-spacing: 0.25rem;
    color: #999;
    border: #999 0.1rem solid;
}
#jump {
    outline: none;
    border: none;
    width: 2rem;
    text-align: center;
    font-size: 0.9rem;
}
.check {
    background-color: pink;
    color: aliceblue;
}
</style>
