<template>
    <div class="backGround fixed -z-100 w-full h-full bg-cover bg-no-repeat bg-center bg-fixed blur-[2px]" :style="{'backgroundImage': bgUrl}"></div>
    <div class="landSpace absolute top-0 left-0 w-full h-full flex flex-col">
        <div class="fixed top-0 left-0 w-full h-16 bg-black text-white flex items-center justify-center">
            <h1 class="text-4xl">FOV_RGT</h1>
        </div>
        <div class="flex-1 flex flex-col items-center justify-center space-y-8">
            <p class="text-6xl">It's MyGO!!!!!</p>
            <p class="text-4xl">即使迷茫也要前进!</p>
            <p>{{ count }}</p>
            <Button variant="outline" @click="increment">click</Button>
        </div>
    </div>
</template>

<script setup lang="ts">
import { Button } from '@/components/ui/button'
import { ref, onMounted } from 'vue'
// @ts-ignore
import * as utils from './assets/componentUtils.js'



const count = ref(0);
const bgUrl = ref('');
function increment(): void {
    count.value++;
}

onMounted(() => {
    const url = ['/gbc.png', '/anon.png'];
    const value = utils.randomIntegerInRange(0,1);
    bgUrl.value = `url(${url[value]})`;
})
</script>

<style scoped>
@import url('../src/assets/App.css');
</style>
