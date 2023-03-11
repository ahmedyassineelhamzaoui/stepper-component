<script >
import FirstComponent from './components/FirstComponent.vue'
import SecondComponent from './components/SecondComponent.vue'
import ThirdComponent from './components/ThirdComponent.vue'
export default {
  components:{
    FirstComponent,
    SecondComponent,
    ThirdComponent,
  },
  
  data() {
    return {
      hideButtons: false,
      message: false,
      currentStep: 0,
      steps: ['1', '2', '3'],
      completedSteps: [false, false, false],
      componentList:['FirstComonent','SecondComponent','ThirdComponent'],
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
        this.completedSteps[this.currentStep-1] = false;
        this.currentStep--
      }
    },
    nextStep() {
      if (this.currentStep < this.steps.length - 1) {
        this.hideButtons=true;
        this.completedSteps[this.currentStep] = true;
        this.currentStep++
      }
    },  
  },
  // mounted() {
  //   this.$on('hide-buttons', (value) => {
  //     this.hideButtons = value;
  //   });
  // }
}
</script>

<template>
  <div class="w-full flex justify-center dark:bg-slate-600 h-screen page-content">
    <div class="w-[90%] sm:w-[90%]">
      <div class="steper-componnet">
        <div class="progress-empty" >
            <div class="progress-full" :style="{ width: progressPercent }"></div>
        </div>
        <div class="cercles-steper">
          <span v-for="(step, index) in steps" :key="index" class="circle" :class="{ active: index === currentStep, completed: completedSteps[index] }">
            {{ completedSteps[index] ? '✔' : step }}
          </span>
        </div>
      </div>
      <div v-if="currentStep==0">
        <FirstComponent></FirstComponent>
      </div>
      <div v-else-if="currentStep == 1">
        <SecondComponent :hideButtons="hideButtons"></SecondComponent>
      </div>
      <div v-else>
        <ThirdComponent></ThirdComponent>
      </div>
      
      <div class="w-full flex justify-between my-bottons"  v-if="!hideButtons" >
        <button  @click="previousStep" class="px-2.5 py-1 border-2 border-gray-800 rounded-sm font-bold bg-gray-700 text-white hover:bg-gray-800 hover:dark:bg-gray-200 dark:bg-white dark:text-gray-700">Previous</button>
        <button  @click="nextStep" class="px-2.5 py-1 border-2 border-gray-800 rounded-sm font-bold bg-gray-700 text-white hover:bg-gray-800 hover:dark:bg-gray-200 dark:bg-white dark:text-gray-700">Next</button>
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
  top: 21px;
  z-index: -1;
}
.progress-full {
  height: 100%;
  background-color: #ff9900;
  transition: 0.5s;
}
.steper-componnet .cercles-steper {
  z-index:0;
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
  margin-left: 20%;
  width: 60%;
}
.circle.active {
  background-color: #ff9900;
  color: black;
}

.buttons {
  display: flex;
  justify-content: space-between;
}
.circle {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  border: 2px solid #ff9900;
  background-color: black;
  font-weight: bold;
  display: flex;
  color: #ff9900;
  justify-content: center;
  align-items: center;
}
</style>