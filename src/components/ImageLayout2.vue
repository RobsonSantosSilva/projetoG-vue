<template>
    <div class="image-layout" v-b-hover="handleHover">
        <img :src="emojiHD" alt="emoji" class="emoji">
        <h1>A fortuna fica ao lado daquele que ousa.</h1>
        <p>Todo progresso ocorre fora da zona de conforto.</p>
           
        <div class="gradient-square">
            <img v-if="isHovered" :src="darkGradient" alt="">        
            <img v-else :src="gradientSquare" alt="">      
        </div>
            
        <div class="square">
            <img v-if="isHovered" :src="whiteSquare" alt="">
            <img v-else :src="blackSquare" alt="">
        </div>
    </div>
</template>

<script>

import emojiHD from '@/assets/emojiHD.png';
import blackSquare from '@/assets/blackSquare.png';
import whiteSquare from '@/assets/whiteSquare.png';
import gradientSquare from '@/assets/gradientSquare.png';
import darkGradient from '@/assets/darkGradient.png';

export default {
    data(){
        return {
            emojiHD, blackSquare, whiteSquare, gradientSquare, darkGradient, isHovered: false
        }
       },
       
        methods: {
            handleHover(hovered) {
            this.isHovered = hovered
        }
        },
 

}

</script>

<style lang="scss" scoped>
.image-layout {
    background-color: #F7F7F7;
    width: 609px;
    height: 599px;
    position: absolute;
    top: 29px;
    left: 610px;
}

.image-layout:hover{
    color: white;
    transition-duration: .5s;
    background-color: black;

    .emoji{
        transform: translate(0px, 32px);
        transition-duration: .5s;
    }
}

.image-layout > h1 {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    font-weight: 700;
    font-size: 24px;
    position: absolute;
    top: 291px;
    left: 76px;
}

.image-layout > p {
    position: absolute;
    top: 342px;
    left: 76px;
    font-weight: 400;
    font-size: 16px;
}

.emoji {
    height: 48px;
    width: 48px;
    position: absolute;
    top: 91px;
    left: 96px;
    transition: transform 0.1s
}

.square {
    position: absolute;
    top: 459px;
    left: 211px;
}


.gradient-square {
    position: absolute;
    top: 470px;
    left: 76px;
}
</style>>

