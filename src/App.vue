<script setup>
import { ref } from 'vue'

const cellsCount = 25

let cells = ref([])

for (let i = 0; i < cellsCount; i++) {
    cells.value.push({
        id: i,
        content: '',
        isBuilt: '',
        buildPercent: 0,
    })
}

function build(id) {
    let cell = cells.value[id]
    let time = 5000
    if (!cell.isBuilt) {
        cell.content = './components/images/home.png'
        cell.isBuilt = 'buildingHouse'
        let increasePercent = setInterval(() => {
            cell.buildPercent += 1
        }, time / 100)
        setTimeout(() => {
            cell.isBuilt = 'builtHouse'
            clearInterval(increasePercent)
        }, time)
    }
}

</script>

<template>
    <div class="h-[100%] w-[100%] p-[10px]">
        <div class="grid grid-cols-5 grid-rows-5 h-[100%] justify-center items-center w-[100%]">
            <div v-for="cell of cells" :key="cell" class="border-[1px] border-black flex flex-col h-[170px] w-[170px] items-center justify-center justify-self-center cursor-pointer hover:opacity-[.5] box-border relative" @click="build(cell.id)">
                <img v-if="cell.content" src="./components/images/home.png" alt="" height="75" width="75" :class="cell.isBuilt">
                <div v-if="cell.isBuilt === 'buildingHouse'" class="absolute left-[50%] translate-x-[-50%] bottom-[5px] rounded-full border-[1px] border-black w-[80%] h-[10%]">
                    <div :style="{ width: cell.buildPercent + '%' }" class="h-[100%] bg-black rounded-full"></div>
                </div>
            </div>
        </div>
    </div>
</template>
<!-- <template>
    <div class="w-[100%] h-[100%] bg-zinc-900 grid grid-cols-3 grid-rows-5 p-[50px]">
        <button class="btn hover:scale-110">button</button>
        <button class="btn hover:scale-90">button</button>
        <button class="btn hover:animate-bounce">button</button>
        <button class="uppercase w-fit h-fit text-white px-[60px] py-[20px] rounded bg-gradient-to-r from-blue-500 to-emerald-500 hover:shadow-[-20px_0px_50px_-10px_#3b82f6,20px_0px_50px_-10px_#10b981] transition-[.5s]">button</button>
        <button class="btn hover:shadow-none">button</button>
        <button class="btn hover:from-translate-x-[-25px] hover:to-translate-x-[50px]">button</button>
        <button class="btn hover:animate-spin">button</button>
        <button class="btn hover:scale-90">button</button>
        <button class="btn hover:scale-90">button</button>
        <button class="btn hover:scale-90">button</button>
        <button class="btn hover:scale-90">button</button>
        <button class="btn hover:scale-90">button</button>
        <button class="btn hover:scale-90">button</button>
        <button class="btn hover:scale-90">button</button>
        <button class="btn hover:scale-90">button</button>
    </div>
</template> -->