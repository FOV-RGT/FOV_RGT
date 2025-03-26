<template>
    <div class="landAnimate fixed h-full w-full z-[1000] bg-black">
        <div class="fixed bottom-0 left-0 w-full h-1/5 bg-black text-white flex items-end justify-start pb-4 pl-4 pr-[10dvw]">
            <h1 class="text-8xl">FOV_RGT</h1>
            <Progress v-model="progress" class="w-full" />
        </div>
    </div>
    <div class="backGround fixed -z-100 w-full h-full bg-cover bg-no-repeat bg-center bg-fixed blur-[2px]"></div>
    <div class="landSpace absolute top-0 left-0 w-full h-full flex flex-col">
        <div class="fixed top-0 left-0 w-full h-16 bg-black text-white flex items-center justify-center">
            <h1 class="text-4xl">FOV_RGT</h1>
        </div>
        <div class="flex-1 flex flex-col items-center justify-center space-y-8">
            <p class="text-6xl">It's MyGO!!!!!</p>
            <p class="text-4xl">即使迷茫也要前进!</p>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref, onMounted, watch } from 'vue'
// @ts-ignore
import * as utils from './assets/componentUtils.js'
import gsap from 'gsap'
import { CustomEase } from "gsap/CustomEase";
import { RoughEase, SlowMo } from "gsap/EasePack";
import { Flip } from "gsap/Flip";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { ScrollToPlugin } from "gsap/ScrollToPlugin";
import { Draggable } from "gsap/Draggable";

import { Progress } from '@/components/ui/progress'


const progress = ref(0);


onMounted(() => {
    gsap.registerPlugin(Flip, ScrollTrigger, ScrollToPlugin, Draggable, RoughEase, SlowMo, CustomEase);
    randomLoadProgress(5, 2000, progress);
})

function randomLoadProgress(step: number, totalTimeout: number, target: any): void {
    let randomArray1 = [];
    let randomArray2 = [];
    let total1 = 0;
    let total2 = 0;
    for (let i = 0; i < step; i++) {
        const random1 = Math.random();
        const random2 = Math.random();
        total1 += random1;
        total2 += random2;
        randomArray1.push(random1);
        randomArray2.push(random2);
    }
    _randomLoad(randomArray1, randomArray2, target, 0, total1, total2, totalTimeout, step);
    watch(progress, (value) => {
        console.log("当前进度", value);
        
        if (value >= 100) {
            setTimeout(() => {
                gsap.to('.landAnimate', { duration: 1, y: '-100%', ease: 'power2.inOut' });
            }, 1000);
        }
    })
}

function _randomLoad(
    progressArray: Array<number>,
    timeoutArray: Array<number>,
    target: any,
    i: number,
    total1: number,
    total2: number,
    totalTimeout: number,
    step: number
): void {
    const time = (timeoutArray[i]/ total2) * totalTimeout;
    const timeOut = setTimeout(() => {
        target.value += (progressArray[i] / total1) * 100;
        if (i + 1 === step) {
            target.value = 100;
            clearTimeout(timeOut);
        } else {
            _randomLoad(progressArray, timeoutArray, target, ++i, total1, total2, totalTimeout, step);
        }
    }, time);
}

</script>

<style scoped>
@import url('../src/assets/App.css');
</style>
