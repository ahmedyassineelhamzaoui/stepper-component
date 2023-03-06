<script >
</script>

<template>
  <div class="w-full flex justify-center dark:bg-slate-600 h-screen page-content">
    <div class="w-[90%] sm:w-[70%]">
      <div class="steper-componnet">
        <div class="progress-empty">
            <div class="progress-full"></div>
        </div>
        <div class="cercles-steper">
            <span class="cercle">1</span>
            <span class="cercle">2</span>
            <span class="cercle">3</span>
        </div>
      </div>
      <div class="w-full flex justify-between">
        <button class="px-2.5 py-1 border-2 border-gray-800 rounded-sm font-bold bg-gray-700 text-white hover:bg-gray-800 hover:dark:bg-gray-200 dark:bg-white dark:text-gray-700">Previous</button>
        <button class="px-2.5 py-1 border-2 border-gray-800 rounded-sm font-bold bg-gray-700 text-white hover:bg-gray-800 hover:dark:bg-gray-200 dark:bg-white dark:text-gray-700">Next</button>
      </div>
    </div>
  </div>
</template>

<style>
.page-content{
  z-index: -2;
}
.steper-componnet .progress-empty {
  background-color: #000a07 !important;
  border-radius: 10px;
  height: 4px;
  width: 60%;
  margin-left: 20%;
  position: relative;
  top: 21px;
  z-index: -1;
}
.steper-componnet .progress-empty .progress-full {
  width: 0%;
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
.steper-componnet .cercles-steper .cercle {
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
