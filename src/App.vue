<script setup lang="ts">
  import { ref } from 'vue';
  
  const showForm = ref<boolean>(false);
  const newTitle = ref<string>("");
  const newMemo = ref<string>("");
  const memos = ref<{ id:number, title:string, content:string, date:string}[]>([]);

  function saveMemo() {
    memos.value.push({
      id: Date.now(),
      title: newTitle.value,
      content: newMemo.value,
      date: new Date().toLocaleDateString(),
    });
    newMemo.value = "";
    newTitle.value = "";
    showForm.value = false;
  }

</script>
<template>
  <main class="items-center justify-center h-full mx-0 my-auto">
    <div class="mx-20">

      <!-- Navbar -->
      <header class="flex justify-between items-center py-5">
        <h1 class="text-2xl font-bold">MEMO</h1>
        <button @click="showForm = true" class="text-2xl rounded-full bg-indigo-100 w-15 h-15 align-middle hover:bg-indigo-200 cursor-pointer">+</button>
      </header>

      <!-- Cards Content -->
      <section class="grid grid-cols-4 gap-5">
        <div v-for="memo in memos" :key="memo.id" class="bg-indigo-100 rounded-lg px-5 py-4 w-full h-[350px] relative">
          <h3 class="text-xl font-semibold mb-4">{{ memo.title }}</h3>
          <div class="flex flex-col justify-between h-full pb-6 pr-1">
            <p class="overflow-auto h-[225px] no-scrollbar">{{ memo.content }}</p>
            <p class="absolute bottom-4 left-5">{{ memo.date }}</p>
          </div>
        </div>
      </section>

      <section v-if="showForm" class="fixed top-0 left-0 bg-black/50 w-full h-full flex justify-center items-center">
        <div class="relative flex flex-col items-center bg-white rounded-xl p-4">
          <button @click="showForm = false" class="absolute right-2 top-[-3px] text-2xl">&times;</button>
          <textarea v-model="newTitle" name="title" id="title" cols="40" rows="1" class="border-2 rounded-md mt-2 mb-1 p-1" placeholder="Title"></textarea>
          <textarea v-model="newMemo" name="memo" id="memo" cols="40" rows="8" class="border-2 rounded-md m-2 p-1" placeholder="Type Here"></textarea>
          <button @click="saveMemo" class="bg-green-200 hover:bg-green-300 cursor-pointer font-semibold shadow-md w-30 px-2 py-1 mt-2 rounded-md">Save</button>
        </div>
      </section>
    </div>
  </main>
</template>
<style scoped>

.no-scrollbar{
  scroll-behavior: smooth;
  -ms-overflow-style: none; /* IE & Edge */
  scrollbar-width: none;     /* Firefox */
}
.no-scrollbar::-webkit-scrollbar {
  display: none;
}
</style>
