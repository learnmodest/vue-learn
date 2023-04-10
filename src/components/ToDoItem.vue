<template>
    <div class="stack-small" v-if="!isEditing">
      <div class="custom-checkbox">
        <input
          type="checkbox"
          class="checkbox"
          :id="id"
          :checked="isDone"
          @change="$emit('checkbox-changed')" />
        <label :for="id" class="checkbox-label">{{label}}</label>
      </div>
      <div class="btn-group">
        <button type="button" class="btn" @click="toggleToItemEditForm">
          Edit <span class="visually-hidden">{{label}}</span>
        </button>
        <button type="button" class="btn btn__danger" @click="deleteToDo">
          Delete <span class="visually-hidden">{{label}}</span>
        </button>
      </div>
    </div>
    <to-do-item-edit-form
        v-else
        :id="id"
        :label="label"
        @item-edited="itemEdited"
        @edit-cancelled="editCancelled">
    </to-do-item-edit-form>
  </template>
<script>
    import ToDoItemEditForm from "./ToDoItemEditForm";

    export default {
        //reference components
        components: {
            ToDoItemEditForm
        },
        //Props are used to allow parent components to pass data to child components 
        //so that they can be rendered and manipulated in the child component's template.
        props: {
            label: { required: true, type: String},
            done: {default: false, type: Boolean},
            id: {required: true, type: String},
        },
        /**
         * Q:what's the difference between let and data() in vue
         * A:let is a keyword in JavaScript used to declare variables, and it is not directly related to Vue.
         *  When you use let to declare a variable within a Vue component, 
         * that variable can only be used within the component itself and cannot be accessed from the template.
         * On the other hand, data() is a Vue component option that defines the initial data for the component. 
         * It is a function that returns an object, and the properties of this object can be accessed using this 
         * within any part of the component, and can be bound to the view through template syntax.
        */
        data() {
            return {
                isEditing: false
            }
        },
        //
        computed: {
            isDone() {
                return this.done;
            }
        },
        methods: {
            itemEdited(newLabel) {
                //$emit：tell parent a named event occur and deliver a attribute
                this.$emit('item-edited', newLabel);
                this.isEditing = false;
            },
            editCancelled() {
                this.isEditing = false;
            },
            deleteToDo() {
                this.$emit('item-deleted');
            },
            toggleToItemEditForm() {
                this.isEditing = true;
            }
        }
    }
</script>