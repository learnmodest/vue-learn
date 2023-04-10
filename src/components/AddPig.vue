<template>
    <form @submit.prevent="onSubmit">
      <h2 class="label-wrapper">
        <label for="new-todo-input" class="label__lg">
          Want a new pig?
        </label>
      </h2>
      <input
        type="text"
        id="new-todo-input"
        name="new-todo"
        autocomplete="off"
        v-model.lazy.trim="selfIntroduce"
        class="input__lg" />
      <button type="submit" class="btn btn__primary btn__lg">Add pig</button>
    </form>
  </template>
  
<script>
export default {
    methods: {
        onSubmit() {
            if(this.selfIntroduce === "") {
                return "";
            }
            this.$emit('pig-add', this.selfIntroduce)
            this.selfIntroduce=""
        }
    },
    data() {
        return {
            selfIntroduce: "",
        }
    }
}
</script>