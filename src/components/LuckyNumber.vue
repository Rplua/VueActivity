<template>
    <div class="float-end">
        <button class="btn btn-outline-danger" @click="generateRandomNumber()">
            <span v-if="luckyNumber === 0">
                Generate luckyNumber <br />
                Range (1-{{ maxNumber }})
            </span>
            <span v-else>
                LuckyNumber: {{ luckyNumber }} <br />
                Click to generate new lucky Number
            </span>
        </button>
    </div>
</template>

<script>
import { ref, inject } from "vue";

export default {
    name: "LuckyNumber",
    props: {
        maxNumber: {
            type: Number,
            default: 100,
        },
    },
    setup(props) {
        const luckyNumber = ref(0);
        
        const maxNumber = inject("maxLuckyNumber")
        const generateRandomNumber = () => {
            luckyNumber.value = Math.floor(Math.random() * maxNumber.value) + 1;
        };

        return {
            luckyNumber,
            generateRandomNumber,
            maxNumber
        };
    },
};
</script>
