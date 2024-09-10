<script>
import { onUnmounted } from 'vue';
import { watch } from 'vue';

export default {
    emits: ['delete'],
    props: {
        orderObj: {
            type: Object,
            default: () => {
                return {};
            }
        }


    },

    data() {
        return {
            setData: {
                imgUrl: '',
                selectGender: '',
                meal: '',
                check1: false,
                check2: false,
                check3: false,
                check4: false,
                showCard: true,
                nameInput: '',
                idInput: '',
                emailInput: '',
                phoneInput: '',
            },
            all: false,


        };
    },

    watch: {
        'orderObj.contractTime': {
            handler(newValue) {
                if (newValue.length < 3) {
                    this.all = false;
                }
            },
            deep: true,
        },

    },

    // mounted() {
    //     // this.watchClick();
    // },

    // onUnmounted() {
    //     this.isClick = false;
    // },

    methods: {
        setImg(e) {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = (e) => {
                    this.setData.imgUrl = e.target.result;

                }
                reader.readAsDataURL(file);
            }
        },

        // setChecked(e) {
        //     this.setData.check2 = e.target.checked;
        //     this.setData.check3 = e.target.checked;
        //     this.setData.check4 = e.target.checked;
        // },

        deleteCard() {
            // this.setData.showCard = false;
            this.$emit('delete', this.orderObj.id);
        },

        setStorage() {
            sessionStorage.setItem('object', JSON.stringify(this.setData));
            console.log(this.setData);
        },

        putFile(e) {
            const file = e.target.files[0];
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = () => {
                this.orderObj.img = reader.result;
            }
        },

        selectAll(e) {
            const checked = e.target.checked;
            if (checked) {
                this.orderObj.contractTime = ['早上', '中午', '晚上'];
            }
        }
    },
}
</script>

<template>
    <div class="container">
        <label class="item">
            姓名
            <input v-model="orderObj.name" type="text" placeholder="姓名">
        </label>
        <label class="item ">
            <input type="file" @change="putFile">
        </label>
        <div class="item picture">
            <img :src="orderObj.img" alt="selected-img" width="100%" />
        </div>
        <label class=" item">
            身分證字號
            <input v-model="orderObj.idNumber" type="text" placeholder="身分證字號">
        </label>
        <label class="item">
            Email
            <input v-model="orderObj.email" type="email" placeholder="email">
        </label>
        <label class="item">
            手機
            <input v-model="orderObj.phone" type="text" placeholder="手機">
        </label>
        <div class="item">性別</div>
        <div class="wrap-item">
            <!-- <div class="style">性別</div> -->
            <label class="item">
                <input type="radio" value="男性" v-model="orderObj.gender">
                男性
            </label>
            <label class="item">
                <input type="radio" value="女性" v-model="orderObj.gender">
                女性
            </label>
            <label class="item">
                <input type="radio" value="其他" v-model="orderObj.gender">
                其他
            </label>
        </div>
        <div class="item">飲食習慣</div>
        <div class="wrap-item">
            <!-- <div class="style">飲食習慣</div> -->
            <label class="item">
                <input type="radio" value="葷" v-model="orderObj.meal">
                葷
            </label>
            <label class="item">
                <input type="radio" value="素" v-model="orderObj.meal">
                素
            </label>

        </div>
        <div class="item">可連絡時間</div>
        <div class="wrap-item">
            <!-- <div class="style">可連絡時間</div> -->
            <label>
                <input id="select-all" v-model="all" type="checkbox" class="item" @click="selectAll">
                全選
            </label>
            <label>
                <input type="checkbox" v-model="orderObj.contractTime" class="item" value="早上">
                早上
            </label>
            <label>
                <input type="checkbox" v-model="orderObj.contractTime" class="item" value="中午">
                中午
            </label>
            <label>
                <input type="checkbox" v-model="orderObj.contractTime" class="item" value="晚上">
                晚上
            </label>


        </div>
        <button class="btn" @click="deleteCard">刪除</button>

    </div>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    width: 300px;
    background-color: rgb(21, 140, 128);
    padding: 10px;
    margin: 10px;
    border-radius: 8px;
    /* height: 450px; */
}

.item {
    margin: 12px;
    color: white;
    width: 100%;
    height: 20px;
}

.wrap-item {
    display: flex;
    color: white;

}

.style {
    display: flex;
}

.btn {
    margin-top: 50px;
    margin-right: 20px;
    cursor: pointer;
}

.picture {
    width: 90%;
    height: 200px;
    background-color: rgb(16, 55, 45);
    overflow: hidden;
}
</style>