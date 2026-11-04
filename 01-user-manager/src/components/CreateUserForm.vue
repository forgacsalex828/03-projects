<script setup>
import { ref } from 'vue'
const isFormVisible = ref(false)

function showForm() {
    isFormVisible.value = true
}

</script>

<template>
    <button
    v-show="!isFormVisible"
    @click="showForm">Create new User</button>
<form
v-show="isFormVisible"
 action="">
            <div class="mb-3">
              <label for="firstName">First Name</label>
              <input class="form-control" type="text" name="firstName" id="firstName" required/>
            </div>

            <div class="mb-3">
              <label for="lastName">Last Name</label>
              <input class="form-control" type="text" name="lastName" id="lastName" required/>
            </div>

            <div class="mb-3">
              <label for="emailAdress">E-mail</label>
              <input class="form-control" type="text" name="emailAdress" id="emailAdress" required/>
            </div>
          </form>

</template>