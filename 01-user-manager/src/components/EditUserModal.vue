<script setup>
import { defineProps, ref, watch } from 'vue';
import { useUserStore } from '../../store/user.js'

const props = defineProps( {
  user: {
    type: Object,
    required: true
  }
})

const closeButton = ref()

const userFormData = ref({ ...props.user })
const { modifyUser } = useUserStore()

function selectInputText(event) {
  event.target.select()
}

watch (
  () => props.user,
  (newUser) => { userFormData.value = { ...newUser } },
  { immediate: true }
)


async function handleSaveButtonClick() {
  try {
    await modifyUser(userFormData.value)
    closeButton.value.click()
  } catch (error) {
    alert(error.message)
  }
}

</script>

<template>
  <!-- Modal -->
  <div
    class="modal fade"
    id="editUserModal"
    tabindex="-1"
    aria-labelledby="editUserModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h4 class="modal-title fs-5" id="editUserModalLabel">Edit user</h4>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <form action="">
            <div class="mb-3">
              <label for="firstName">First Name</label>
              <input class="form-control" type="text" name="firstName" id="firstName" required
              v-model="userFormData.firstName" @focus="selectInputText" />
            </div>

            <div class="mb-3">
              <label for="lastName">Last Name</label>
              <input class="form-control" type="text" name="lastName" id="lastName" required 
               v-model="userFormData.lastName" @focus="selectInputText"/>
            </div>

            <div class="mb-3">
              <label for="emailAdress">E-mail</label>
              <input class="form-control" type="text" name="emailAdress" id="emailAdress" required 
               v-model="userFormData.emailAdress" @focus="selectInputText"/>
            </div>
          </form>

        </div>
        <div class="modal-footer">
          <button ref="closeButton" type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
          <button type="button" class="btn btn-primary"
          @click="handleSaveButtonClick">Save changes</button>
        </div>
      </div>
    </div>
  </div>
</template>
