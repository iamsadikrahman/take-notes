<script setup>
import {onBeforeMount, onMounted, reactive, ref} from "vue";

import {Modal} from "flowbite-vue";


const isShowModal = ref(false)

function closeModal() {
  isShowModal.value = false
}

function showModal() {
  isShowModal.value = true
}


const notes = reactive([])

console.log(notes)


const getNote = ref("")

function noteColor() {
  const randomColor = `rgb(${Math.floor(Math.random()* 255)}, ${Math.floor(Math.random()* 255)}, ${Math.floor(Math.random()* 255)}, 0.7)`
  console.log(randomColor)
  return randomColor
}

function newNote() {
  notes.push({
    id: Math.floor(Math.random() * 100000),
    noteText: getNote.value,
    color: noteColor(),
    date: new Date()


  })
  isShowModal.value = false
  getNote.value = ''
}

function removeNote(index){
  notes.splice(index, 1)
}

// function editNote(index) {
//   isShowModal.value = true
// }





// const pinNote = (index) => {
//   const pinnedNote = notes.splice(index, 1)[index]
//   notes.unshift(pinnedNote)
// }


// function updateNote(index) {
//   isShowModal.value = true
//   getNote.value = notes[index].noteText
//   notes[index].color = noteColor()
//
// }


let showEdit = ref(false)

let editNote = ref('')
console.log(editNote)

function editNoteFunc(index) {

    showEdit.value = true
    notes[index].noteText = getNote.value
    console.log(getNote.value)


}



</script>

<template>
  <section>
    <header class="flex justify-between p-4 bg-gray-200 rounded mb-4 ">
      <h1 class="text-4xl font-bold text-gray-800 mb-4 ">Notes</h1>
      <button @click="showModal" class="bg-blue-500 text-white px-4 py-2 rounded text-2xl" type="button">Take Notes+
      </button>
    </header>
    <main>
      <Modal :size="size" v-if="isShowModal" @close="closeModal">
        <template #header>
          <div class="flex items-center text-lg">
            Write Your Note...
          </div>
        </template>
        <template #body>
          <textarea v-model="getNote" id="note" cols="60" rows="10"></textarea>
        </template>
        <template #footer>
          <div class="flex justify-between flex-col space-y-4">
            <button @click="newNote" type="button"
                    class="text-gray-500 bg-white hover:bg-gray-100 focus:ring-4 focus:outline-none focus:ring-blue-300 rounded-lg border border-gray-200 text-sm font-medium px-5 py-2.5 hover:text-gray-900 focus:z-10 dark:bg-gray-700 dark:text-gray-300 dark:border-gray-500 dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-gray-600">
              Add Note
            </button>
            <button @click="closeModal" type="button"
                    class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
              Cencel
            </button>
          </div>
        </template>
      </Modal>

      <section class="flex space-x-4 flex-wrap">
        <div v-for="(note, index) in notes" :key="index" class="border p-5 rounded-lg h-[400px] w-[400px] flex flex-col justify-between overflow-auto " :style="{backgroundColor: note.color}">
          <p @click="" >{{ note.noteText }}</p>
          <input v-if="showEdit" v-model="getNote" type="text" name="" id="">
          <p>{{note.date.toLocaleDateString()}}</p>
          <button @click="editNoteFunc(index)" type="button" class="border p-2 bg-black text-white">Edit</button>
          <button @click="removeNote(index)" class="border p-2 bg-black text-white" type="button">Delete</button>
          <button class="border p-2 bg-black text-white" type="button"> Pin it</button>
        </div>
      </section>


    </main>
  </section>
</template>

<style scoped>


</style>
