<script >
import "@fortawesome/fontawesome-free/css/all.css";

import FirstComponent from './components/FirstComponent.vue'
import SecondComponent from './components/SecondComponent.vue'
import ThirdComponent from './components/ThirdComponent.vue'
export default {
  components: {
    FirstComponent,
    SecondComponent,
    ThirdComponent,
  },

  data() {
    return {
      Myscore: 0,
      questions: [],
      hideButtons: false,
      currentStep: 0,
      steps: ['1', '2', '3'],
      completedSteps: [false, false, false],
      componentList: ['FirstComonent', 'SecondComponent', 'ThirdComponent'],
    }
  },
  computed: {
    progressPercent() {
      return (this.currentStep / (this.steps.length - 1)) * 100 + '%'
    },
  },
  methods: {
    previousStep() {
      if (this.currentStep > 0) {
        this.completedSteps[this.currentStep - 1] = false;
        this.currentStep--
      }
    },
    nextStep() {
      
      if (this.currentStep < this.steps.length - 1) {
        this.completedSteps[this.currentStep] = true;
        this.currentStep++
      }
      if(this.currentStep==2){
        document.querySelector('.next-btn').innerHTML="<a href=''>take another quiz</a>"
      }
    },
    handleStatusChange(newStatus, score, newQuestions) {
      this.hideButtons = newStatus
      this.Myscore = score
      this.questions = newQuestions;
      console.log(newQuestions)
    },   
    isWrongAnswer(wrongAnswear,i){
      for(let j=0;j<wrongAnswear.selectedChoices.length;j++){
        if(wrongAnswear.question.choices[i].id === wrongAnswear.selectedChoices[j]){
          return true
        }
      }
    },
    isCorrectAnswer(wrongAnswear,i) {
      return  wrongAnswear.question.choices[i].id === wrongAnswear.question.correctAnswear;                                                                                                                             
    },
  },



}
</script>

<template>
  <div class="w-full flex justify-center dark:bg-slate-600 h-screen page-content">
    <div class="w-[90%] sm:w-[90%]">
      <div class="steper-componnet">
        <div class="progress-empty">
          <div class="progress-full" :style="{ width: progressPercent }"></div>
        </div>
        <div class="cercles-steper">
          <span  v-for="(step, index) in steps" :key="index" class="circle"
            :class="{ active: index === currentStep, completed: completedSteps[index] } ">
            {{ completedSteps[index] ? '✔' : step }}
          </span>
        </div>
      </div>
      <div v-if="currentStep == 0">
        <FirstComponent></FirstComponent>
      </div>
      <div v-else-if="currentStep == 1">
        <SecondComponent v-on:changeStatus="handleStatusChange"></SecondComponent>
      </div>
      <div v-else>
        <ThirdComponent></ThirdComponent>
        <h2 class="text-center font-bold">Your score is : <span>{{ this.Myscore }}</span> / <span>10</span> </h2>
        <div v-for="wrongAnswear in this.questions" :key="wrongAnswear.question">
          <div
            class="w-full mb-4 p-6 text-sky-900 bg-white border border-gray-200 rounded-lg shadow-md dark:bg-gray-800 dark:border-gray-700 ">
            <p class="font-bold flex flex-start text-stone-800  text-md">The Question:{{ wrongAnswear.question.text }}</p>
            <p class="flex font-sans  items-center text-md"  
            :class="{
              'text-green-600': isCorrectAnswer(wrongAnswear, 0),
              'text-red-600': isWrongAnswer(wrongAnswear,0)  && !isCorrectAnswer(wrongAnswear, 0),
           }">
            <i
                class="fa-solid fa-circle-dot mr-2" ></i><span>{{ wrongAnswear.question.choices[0].text }}
              </span></p>
            <p class="flex font-sans  items-center text-md"
            :class="{
              'text-green-600': isCorrectAnswer(wrongAnswear,1),
              'text-red-600': isWrongAnswer(wrongAnswear,1)  && !isCorrectAnswer(wrongAnswear, 1),

            }">
            <i
                class="fa-solid fa-circle-dot mr-2"></i><span>{{ wrongAnswear.question.choices[1].text }}
              </span></p>
            <p class="flex font-sans  items-center text-md" 
            :class="{
              'text-green-600': isCorrectAnswer(wrongAnswear,2),
              'text-red-600': isWrongAnswer(wrongAnswear,2)  && !isCorrectAnswer(wrongAnswear, 2),

            }">
            <i
                class="fa-solid fa-circle-dot mr-2"></i><span>{{ wrongAnswear.question.choices[2].text }}
              </span></p>
            <p class="flex font-sans  items-center text-md" 
            :class="{
              'text-green-600': isCorrectAnswer(wrongAnswear,3),
              'text-red-600': isWrongAnswer(wrongAnswear,3)  && !isCorrectAnswer(wrongAnswear, 3),
            }"
            ><i
                class="fa-solid fa-circle-dot mr-2"></i><span>{{ wrongAnswear.question.choices[3].text }}
              </span></p>
          </div>
          <div
            class="w-full mb-4 p-6 bg-white border border-gray-200 rounded-lg shadow-md dark:bg-gray-800 dark:border-gray-700">
            <h1 class="flex items-center">
              <span class="mr-2 text-yellow-400">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                  stroke="currentColor" class="w-6 h-6">
                  <path stroke-linecap="round" stroke-linejoin="round"
                    d="M11.25 11.25l.041-.02a.75.75 0 011.063.852l-.708 2.836a.75.75 0 001.063.853l.041-.021M21 12a9 9 0 11-18 0 9 9 0 0118 0zm-9-3.75h.008v.008H12V8.25z" />
                </svg>
              </span>
              <span class="text-xl text-amber-500">Explnation</span>
            </h1>
            <p class="flex font-sans font-bold items-center text-cyan-900 text-md">{{ wrongAnswear.question.explanation }}
            </p>
          </div>
        </div>

      </div>

      <div class="w-[80%] mx-auto  flex justify-between  my-bottons" v-if="!hideButtons">
        <button @click="previousStep"
          class="previous px-2.5 py-1 border-2 border-gray-800 rounded-sm font-bold bg-gray-700 text-white hover:bg-gray-800 hover:dark:bg-gray-200 dark:bg-white dark:text-gray-700">Previous</button>
        <button @click="nextStep"
          class="next-btn px-2.5 py-1 border-2 mb-2 border-gray-800 rounded-sm font-bold bg-gray-700 text-white hover:bg-gray-800 hover:dark:bg-gray-200 dark:bg-white dark:text-gray-700">Next</button>
      </div>

    </div>
  </div>
</template>

<style>
.progress-empty {
  background-color: #000a07 !important;
  border-radius: 10px;
  height: 4px;
  width: 60%;
  margin-left: 20%;
  position: relative;
  top: 26px;
  z-index: -1;
}

.progress-full {
  height: 100%;
  background-color: #ff9900;
  transition: 0.5s;
}

.steper-componnet .cercles-steper {
  z-index: 0;
  display: flex;
  justify-content: space-between;
  margin-bottom: 4em;
  margin-left: 20%;
  width: 60%;
}

.circle.active {
  background-color: #ff9900;
  color: black;
  font-weight: bolder;
}

.buttons {
  display: flex;
  justify-content: space-between;
}

.circle {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  border: 2px solid #ff9900;
  background-color: black;
  font-weight: bold;
  display: flex;
  color: #ff9900;
  justify-content: center;
  align-items: center;
}
.previous{
  visibility: hidden;
}
</style>