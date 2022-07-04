<template>
  <div>
    <GetBook></GetBook>
    <br>
    <AddBook></AddBook>
  </div>
</template>

<script>
import GetBook from './components/GetBook.vue'
import AddBook from './components/AddBook.vue'
export default {
  data() {
    return {
      book: []
    }
  },
  components: {
    GetBook,
    AddBook
  },
  methods: {
    
  }
}
</script>

<style>
</style>