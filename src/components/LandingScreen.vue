<template>
    <div class="main-container">
        <img src="../assets/BlueBall.png" class="blue-circle">
        <HeaderComponent></HeaderComponent>
        <div class="content-container">
            <h1 class="main-text">
                <span style="color:#FF493B; font-weight: 700;">AI</span>-агрегатор
                <br>фриланс-заказов
                <br>для дизайнеров
            </h1>
            <div class="button-container">
                <v-btn 
                color="black" 
                size="large" 
                rounded="xl" 
                variant="flat"
                class="form-button">
                    Попробовать бесплатно
                    <template #append>
                        <img 
                        src="../assets/CoralArrow.svg" 
                        alt="" 
                        class="button-icon">
                    </template>
                </v-btn>

                <v-btn 
                color="#FF493B" 
                size="large" 
                rounded="xl" 
                variant="flat"
                class="form-button"
                style="flex:0.6">
                    Узнать больше
                </v-btn>
            </div>
        </div>
        
    </div>

</template>

<script setup>
import HeaderComponent from './HeaderComponent.vue';
</script>

<style scoped>

.main-container {
    min-height: 300vh;
    width: 100vw;
    background-color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.button-container {
    width: 600px;
    margin-top: 2rem;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    gap: 1rem;
}

.button-icon {
    margin-left: 0.5rem;
    width: 1rem;
    height: 1rem;
}

.content-container {
    margin-top : var(--header-container-height);
    z-index: 20;
    height: 400px;
    width: 75%;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.main-text {
    margin-top: 2rem;
    font-size: 3.5rem;
    font-weight: 500;
}

.blue-circle{
    z-index:0;
    position: absolute;
    height: 175vh;
    aspect-ratio: 1;
    border-radius: 100%;
    filter: blur(2px);
    transform: translateY(-45%)
}

.form-button {
  flex: 1;
  /* padding: 0 2rem 0 2rem; */
  transition: padding 0.2s ease-in-out;
}

.form-button:hover {
  padding: 0 3rem 0 3rem;
}
</style>
