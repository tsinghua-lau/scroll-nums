<template>
    <div class="counter">
    <span v-for="(item,index) in computeNumber">
      <i ref="numberItem">0123456789</i>
    </span>
    </div>
</template>
<script>

    export default {
        name: "SaleCounter",
        props: {
            currentList: Number
        },
        data() {
            return {
                computeNumber: [0,0,0,0,0,0]
            };
        },
        watch: {
            currentList(newVal) {
                let that = this;
                that.computeNumber = that.numToArr(newVal, 6);
                that.setNumberTransform();
            }

        },
        created() {

        },
        mounted() {

        },
        methods: {

            getRandomNumber(min, max) {
                return Math.floor(Math.random() * (max - min + 1) + min);
            },
            setNumberTransform() {
                let numberItems = this.$refs.numberItem;
                let numberArr = this.computeNumber.filter(item => !isNaN(item));
                for (let index = 0; index < numberItems.length; index++) {
                    let elem = numberItems[index];
                    elem.style.transform = `translate(-50%, -${numberArr[index] * 10}%)`;
                }
            },
            //数字转数组
            numToArr(num, count) {
                let numArr = [];
                let i;
                for (i = 0; i < count; i++) {
                    numArr.push(Math.floor(num / Math.pow(10, count - i - 1)) % 10);
                }
                return numArr;
            }
        }
    };
</script>
<style scoped>
    .counter {
        display: inline-block;
        height: 36px;
        margin-left: 12px;
    }

    .counter span {
        margin-left: 3px;
        height: 30px;
        width: 22px;
        line-height: 22px;
        display: inline-block;
        position: relative;
        overflow: hidden;
        background: url("../assets/img/counterback.png");
        color: #def5e9;
        font-size: 18px;
        writing-mode: vertical-lr;
        text-orientation: upright;
    }

    .counter span > i {
        position: absolute;
        top: 20%;
        left: 50%;
        transform: translate(-50%, 0);
        transition: transform 0.5s ease-in-out;
        letter-spacing: 10px;
        font-style: normal;
        line-height: 30px;
    }

    .counter span:nth-of-type(4) {
        margin-left: 8px;
    }
</style>