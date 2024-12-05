<script setup>
// import { RouterLink, RouterView } from "vue-router";
import { ref } from 'vue'

let count = ref(0)
let canBoost = ref(true)
let increaseValue = 1

function increaseCount() {
    count.value += increaseValue
}

function boost() {
    rechargeBoost()
    let boosting = setInterval(() => {
        count.value += increaseValue
    }, 80)
    setTimeout(() => {
        clearInterval(boosting)
    }, 5000)
}

function rechargeBoost() {
    canBoost.value = false
    setTimeout(() => {
        canBoost.value = true
    }, 30000)
}

</script>

<template>
    <div class="flex flex-col items-center h-[100%]">
        <div class="flex flex-col items-center">
            <div class="my-[50px] text-[250px]">{{ count }}</div>
            <button class="border-[1px] border-black mb-[10px] h-[70px] w-[70px] rounded-full h-fit w-fit hover:opacity-[.8] active:animate-ping" @click="increaseCount()">+1</button>
            <button class="border-[1px] border-black h-[50px] w-[50px] p-[10px] text-[10px] rounded-full h-fit w-fit hover:opacity-[.8] active:animate-ping disabled:animate-none disabled:opacity-[.5]" :disabled="!canBoost" @click="boost()">boost</button>
        </div>
    </div>
</template>