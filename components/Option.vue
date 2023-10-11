<template>
    <div class="option-container">
        <h3>{{ option.title }}</h3>
        <div class="option-buttons">
            <button 
            v-for="value in Option.buttons" :key="value"
            :class="options[option.category] === value && 'active'" 
            @click="options[option.category]=value"
            >
                {{ value }}
            </button>
        </div>
    </div>
</template>

<script setup lang="ts">
    import { Gender,Popularity,Length } from '@/data'

    interface OptionProps {
        option: {
            title: string,
            category: string,
            buttons: Gender[] | Popularity[] | Length[]
        },
        options: {
            gender: Gender,
            popularity: Popularity,
            length: Length
        }
    }

    const props = defineProps<OptionProps>()

</script>

<style lang="scss" scoped>

</style>