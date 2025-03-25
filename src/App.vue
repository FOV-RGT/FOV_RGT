<script setup lang="ts">
import { Button } from '@/components/ui/button'
</script>

<template>
    <div class="landSpace absolute top-0 left-0 w-screen h-screen flex flex-col">
        <div class="fixed top-0 left-0 w-full h-16 bg-[#2D496C] text-white flex items-center justify-center">
            <h1 class="text-4xl">FOV_RGT</h1>
        </div>
        <div class="flex-1 flex flex-col items-center justify-center space-y-8">
            <p class="text-6xl">It's MyGO!!!!!</p>
            <p class="text-4xl">即使迷茫也要前进！</p>
            <Button variant="destructive">click</Button>
        </div>
    </div>
</template>

<style scoped></style>
