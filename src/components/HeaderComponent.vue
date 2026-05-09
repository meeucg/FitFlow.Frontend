<template>
    <div class="header-container">
        <div class="header-body">
            <div class="logo-container">
                <img src="../assets/logo.svg" class="logo"></img>
                <h3 class="text">fitflow.art</h3>
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
</script>

<style scoped>
.text {
    color: black;
    font-weight: 500;
    user-select: none;
}

.header-body {
    max-width: 1000px;
    width: 90%;
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
    justify-content: space-between;
    align-items: center;
    gap: 1rem;
}

.sign-in-container {
    height: 100%;
    width: calc(200px - 1.1rem);
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