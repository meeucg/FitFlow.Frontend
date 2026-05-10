<template>
    <component
        :is="tag"
        ref="elementRef"
        class="reveal-on-active"
        :style="rootStyle"
        :aria-hidden="active ? undefined : 'true'"
        :inert="active ? undefined : true"
    >
        <slot></slot>
    </component>
</template>

<script setup lang="ts">
import { computed, onBeforeUnmount, onMounted, ref, watch } from 'vue';
import { gsap } from 'gsap';

type CssLength = string | number;

const props = withDefaults(defineProps<{
    active?: boolean;
    tag?: string;
    y?: CssLength;
    delay?: number;
    duration?: number;
    exitDuration?: number;
    ease?: string;
    exitEase?: string;
    blur?: CssLength;
    appear?: boolean;
}>(), {
    active: true,
    tag: 'div',
    y: 34,
    delay: 0,
    duration: 0.8,
    exitDuration: 0.42,
    ease: 'power3.out',
    exitEase: 'power3.in',
    blur: 4,
    appear: true,
});

const elementRef = ref<HTMLElement | null>(null);
const hasMounted = ref(false);
let currentTween: gsap.core.Tween | null = null;

const toCssLength = (value: CssLength) => (
    typeof value === 'number' ? `${value}px` : value
);

const hiddenVars = computed(() => ({
    opacity: 0,
    y: props.y,
    filter: `blur(${toCssLength(props.blur)})`,
}));

const visibleVars = {
    opacity: 1,
    y: 0,
    filter: 'blur(0px)',
};

const rootStyle = computed(() => ({
    pointerEvents: props.active ? undefined : 'none',
    ...(!hasMounted.value && (props.appear || !props.active)
        ? {
            opacity: 0,
            transform: `translate3d(0, ${toCssLength(props.y)}, 0)`,
            filter: `blur(${toCssLength(props.blur)})`,
        }
        : {}),
}));

const killTween = () => {
    currentTween?.kill();
    currentTween = null;
};

const animateIn = () => {
    const element = elementRef.value;

    if (!element) {
        return;
    }

    killTween();
    currentTween = gsap.fromTo(
        element,
        hiddenVars.value,
        {
            ...visibleVars,
            delay: props.delay,
            duration: props.duration,
            ease: props.ease,
            force3D: true,
            willChange: 'transform, opacity, filter',
        },
    );
};

const animateOut = () => {
    const element = elementRef.value;

    if (!element) {
        return;
    }

    killTween();
    currentTween = gsap.to(element, {
        ...hiddenVars.value,
        duration: props.exitDuration,
        ease: props.exitEase,
        force3D: true,
        willChange: 'transform, opacity, filter',
    });
};

onMounted(() => {
    const element = elementRef.value;

    if (!element) {
        return;
    }

    if (!props.active) {
        gsap.set(element, hiddenVars.value);
    } else if (props.appear) {
        gsap.set(element, hiddenVars.value);
    } else {
        gsap.set(element, visibleVars);
    }

    hasMounted.value = true;

    if (props.active && props.appear) {
        animateIn();
    }
});

watch(
    () => props.active,
    (isActive) => {
        if (!hasMounted.value) {
            return;
        }

        if (isActive) {
            animateIn();
            return;
        }

        animateOut();
    },
);

onBeforeUnmount(killTween);
</script>

<style scoped>
.reveal-on-active {
    display: block;
    will-change: transform, opacity, filter;
}
</style>
