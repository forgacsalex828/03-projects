<script setup>
import { ref } from 'vue'
import { useUserStore } from '../../store/user.js'

const { addUser } = useUserStore()
const isFormVisible = ref(false)
const newUser = ref({
  firstName: '',
  lastName: '',
  emailAdress: '',
})

function showForm() {
  isFormVisible.value = true
}

function resetForm() {
  newUser.value = {
    firstName: '',
    lastName: '',
    emailAdress: '',
  }
}

async function handleSaveClick() {
  const userToCreate = {
    firstName: newUser.value.firstName.trim(),
    lastName: newUser.value.lastName.trim(),
    emailAdress: newUser.value.emailAdress.trim(),
  }

  if (!userToCreate.firstName || !userToCreate.lastName || !userToCreate.emailAdress) {
    return
  }

  try {
    await addUser(userToCreate)
    resetForm()
    isFormVisible.value = false
  } catch (error) {
    console.error('Error creating user:', error)
  }
}

function handleCancelClick() {
  resetForm()
  isFormVisible.value = false
}
</script>

<template>
  <button v-show="!isFormVisible" type="button" @click="showForm">Create new User</button>

  <form v-show="isFormVisible" action="" @submit.prevent="handleSaveClick">
    <div class="mb-3">
      <label for="firstName">First Name</label>
      <input v-model="newUser.firstName" class="form-control" type="text" name="firstName" id="firstName" required />
    </div>

    <div class="mb-3">
      <label for="lastName">Last Name</label>
      <input v-model="newUser.lastName" class="form-control" type="text" name="lastName" id="lastName" required />
    </div>

    <div class="mb-3">
      <label for="emailAdress">E-mail</label>
      <input v-model="newUser.emailAdress" class="form-control" type="text" name="emailAdress" id="emailAdress" required />
    </div>

    <div class="mb-3">
      <button class="btn btn-primary" type="submit">Save</button>
    </div>

    <div class="mb-3">
      <button class="btn btn-secondary" type="button" @click="handleCancelClick">Cancel</button>
    </div>
  </form>
</template>