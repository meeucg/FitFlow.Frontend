<template>
    <article class="bottom-left-card">
        <div class="upper-part">
            <div class="star-icon"></div>
            <SplitText
                tag="h3"
                class="question-text"
                split-type="words"
                :active="active"
            >
                Почему FitFlow удобнее ручного поиска?
            </SplitText>
        </div>
        <div class="lower-part"></div>
    </article>
</template>

<script setup lang="ts">
import SplitText from './SplitText.vue';

withDefaults(defineProps<{
    active?: boolean;
}>(), {
    active: true,
});
</script>

<style scoped>
.bottom-left-card {
    min-height: 265px;
    border-radius: 2rem;
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(32px);
    box-shadow: 0 18px 54px rgba(23, 42, 97, 0.13);
    display: flex;
    flex-direction: column;
    gap: 1rem;
    padding: 1.5rem;
}

.upper-part {
    flex: 1;
    display: flex;
    flex-direction: row;
    justify-content: baseline;
    align-items: center;
    gap: 2rem;
}

.question-text {
    font-size: 1.25rem;
    font-weight: 500;
    line-height: 1.2;
    max-width: 300px;
    color: black
}

.lower-part {
    flex: 2;
    background: white;
    border-radius: 1.5rem;
    box-shadow: 0 12px 36px rgba(17, 57, 177, 0.164);
}

.star-icon {
    width: 4rem;
    box-sizing: border-box;
    aspect-ratio: 1;
    background: url('../assets/Stars.svg') center center no-repeat;
    background-size: contain;
}
</style>
