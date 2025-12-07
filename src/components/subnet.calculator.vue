<template>
    <div class="appContainer">    
        <div class="calculator">
            <form class="form" @submit.prevent="showResult">
                <div>
                    <div class="inputLabel">IP</div>
                    <input class="input" v-model="ip" placeholder="Введите IP (0.0.0.0)"/>
                </div>
                
                <div>
                    <div class="selectLabel">
                        Маска подсети
                    </div>    
                    <select class="select" v-model="mask" :disabled="!isIpValid(ip) && isShowResult">
                        <option v-for="mask in maskList" :key="mask" :value="mask">
                            {{ mask }}
                        </option>
                    </select>
                </div>
                
                <div>
                    <button class="button" type="submit" :disabled="!isIpValid(ip)">
                        Рассчитать
                    </button>
                </div>

            </form>

            <div class="result-container">
                <div class="result" v-if="isShowResult && isIpValid(ip)">
                    <div>IP: {{ip}}</div>
                    <div>Маска подсети: {{mask}}</div>
                    <div>Адрес сети: {{ getNetworkAdress(ip, mask) }}</div>
                    <div>Кол-во адресов: {{ getAddressesCount (mask) }}</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { maskList } from './arrays';
import { isIpValid, getAddressesCount, getNetworkAdress } from './functions';

const ip = ref('')
const mask = ref(maskList[0])
const isShowResult = ref(false)

function showResult(){
    isShowResult.value = true
}
</script>

<style lang="scss">

    .appContainer{
    display: flex;
  justify-content: center;
  align-items: center;
        height: 100%;
    }

    .calculator{
        background-color: var(--color-gray-light); 
        padding: 60px;
        width: 100%;
        max-width: 1200px;
        height: 94.75vh;
    }

    .form{
          display: flex;
            gap: 100px;
            justify-content: center;
    }
    
    .result-container{
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 200px;
    }

    .result{
        color: var(--color-white);
        background-color: var(--color-primary);
        border: 2px solid var(--color-blue-dark);
        border-radius: 10px;
        display: flex;
        justify-content: center;
        flex-direction: column;
        align-items: center;
        gap: 15px;
        padding: 20px;
        font-weight: 600;
    }

    .inputLabel{
        color: var(--color-gray);
        font-weight: 600;
    }

    .selectLabel{
        color: var(--color-gray);
        font-weight: 600;
    }


    .input{
    border: 2px solid var(--color-primary);
    border-radius: 10px;
    font-size: 1em;
    font-weight: 600;
    line-height: 1.5em;
    padding: 10px;
    cursor: pointer;
    width: 25vh;
    height: 5vh;

    &:focus {
        outline: none;
    }
}

.select{
    border: 2px solid var(--color-primary);
    border-radius: 10px;
    font-size: 1em;
    font-weight: 600;
    line-height: 1.5em;
    padding: 10px;
    cursor: pointer;
    width: 25vh;
    height: 5vh;

    &:focus {
        outline: none;
    }
    
    &:disabled{
        cursor: not-allowed;
    }
}

    .button {
        margin-top: 20px;
  color: var(--color-white);
  background-color: var(--color-primary);
  border: none;
  border-radius: 10px;
  height: 50px;
  width: 120px; 
  font-size: 1em;
  font-weight: 600;
  cursor: pointer;
  
  
  &:hover:not(:disabled) {
    background-color: var(--color-blue);
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  }
  
  &:active:not(:disabled) {
    transform: translateY(1px);
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  }
  
  &:disabled {
    background-color: var(--color-gray);
    cursor: not-allowed;
    opacity: 0.6;
  }
}
</style>