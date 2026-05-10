<template>
    <div class="header-container">
        <div
            ref="headerBodyRef"
            class="header-body"
            :style="animateOnMount ? headerInitialStyle : undefined"
        >
            <div class="logo-container">
                <img src="../assets/logo.svg" class="logo"></img>
                <SplitText
                    tag="h3"
                    class="text"
                    split-type="words"
                    :delay="35"
                >
                    fitflow.art
                </SplitText>
            </div>
            <div class="button-container">
                <v-btn 
                    variant="text" 
                    color="black" 
                    rounded="xl">
                    Отзывы
                </v-btn>
                <v-btn 
                    variant="text" 
                    color="black" 
                    rounded="xl">
                    Как это работает?
                </v-btn>
                <v-btn 
                    variant="text" 
                    color="black" 
                    rounded="xl">
                    Тарифы
                </v-btn>
            </div>
            <div class="sign-in-container">
                <v-btn 
                variant="flat" 
                color="black" 
                rounded="xl"
                class="form-button">
                Вход
                </v-btn>
            </div>
        </div>
    </div>
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue';
import { gsap } from 'gsap';
import SplitText from './SplitText.vue';

const props = defineProps({
    animateOnMount: {
        type: Boolean,
        default: true,
    },
});

const headerBodyRef = ref(null);
const headerEnterOffset = -150;
const headerInitialStyle = {
    opacity: 0,
    transform: `translate3d(0, ${headerEnterOffset}px, 0)`,
};

let headerTween = null;

onMounted(() => {
    if (!props.animateOnMount || !headerBodyRef.value) {
        return;
    }

    headerTween = gsap.fromTo(
        headerBodyRef.value,
        {
            opacity: 0,
            y: headerEnterOffset,
        },
        {
            opacity: 1,
            y: 0,
            duration: 0.9,
            ease: 'power3.out',
            force3D: true,
        },
    );
});

onBeforeUnmount(() => {
    headerTween?.kill();
});
</script>

<style scoped>
.text {
    color: black;
    font-weight: 500;
    user-select: none;
}

.header-body {
    max-width: 1000px;
    width: min(90%, 1000px);
    min-width: 0;
    height: calc(100% - 80px);
    margin-top: 40px;
    background: linear-gradient(
        to right in oklch, 
        white, 15%, 
        rgba(255,255,255,0.8),
         85%, 
         white);
    box-sizing: border-box;
    border-radius: var(--header-container-height);
    backdrop-filter: blur(8px);
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    padding-left: 0.8rem;
    padding-right: 1.1rem;
}

.logo-container {
    height: 100%;
    width: calc(200px - 0.8rem);
    min-width: 0;
    flex: 0 1 calc(200px - 0.8rem);
    display: flex;
    flex-direction: row;
    justify-content: baseline;
    align-items: center;
    gap: 1rem;
}

.logo {
    height: calc(100% - 1.6rem);
    aspect-ratio: 1;
    background-color: red;
    border-radius: 100%;
}

.button-container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    flex: 1 1 auto;
    gap: 1rem;
    min-width: 0;
}

.sign-in-container {
    height: 100%;
    width: calc(200px - 1.1rem);
    flex: 0 1 calc(200px - 1.1rem);
    display: flex;
    flex-direction: row;
    justify-content: end;
    align-items: center;
}

.header-container {
    position: fixed;
    display: flex;
    flex-direction: row;
    justify-content: center;
    z-index: 999;
    height: var(--header-container-height);
    width: 100%;
}

.form-button {
  padding: 0 1.5rem 0 1.5rem;
  transition: padding 0.2s ease-in-out;
}

.form-button:hover {
  padding: 0 2rem 0 2rem;
}
</style>
