<template>
    <base-dialog v-if="inputIsInvalid" title="Invalid Input">
        <template #default>
            <p>Unfortunately, at least one input value is invalid.</p>
            <p>Please check all inputs and make sure you enter at least a few characters into each input field.</p>
        </template>
        <template v-slot:actions>
            <base-button @click="confirmError">Okay</base-button>
        </template>
    </base-dialog>
    <base-card>
        <form @submit.prevent="submitData">
            <div class="form-control">
                <label for="title">Title</label>
                <input id="title" name="title" type="text" ref="userTitle">
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <textarea id="description" name="description" rows="3" ref="userDescription"></textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input id="link" name="link" type="url" ref="userLink" required>
            </div>
            <div class="form-control">
                <base-button type="submit">Add Resource</base-button>
            </div>
        </form>
    </base-card>
</template>

<script>
export default {
    data() {
        return {
            inputIsInvalid: false,
        }
    },
    inject: ['addResource'],
    methods: {
        submitData() {
            const enteredTitle = this.$refs.userTitle.value;
            const enteredDescription = this.$refs.userDescription.value;
            const enteredUrl = this.$refs.userLink.value;

            if (enteredTitle.trim() === '' || enteredDescription.trim() === '' || enteredUrl.trim() === '') {
                this.inputIsInvalid = true
                return;
            }

            this.addResource(enteredTitle, enteredDescription, enteredUrl)
        },
        
        confirmError() {
            this.inputIsInvalid = false;
        }
    },
}
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>