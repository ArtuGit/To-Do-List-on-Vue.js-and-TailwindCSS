<template>
  <form class="flex mt-8 mb-2" @submit.prevent="submitTask">
    <input
      v-model="name"
      class="shadow appearance-none border rounded w-full py-2 px-3 mr-4 text-grey-darker"
      placeholder="Add Task"
      type="text"
      maxlength="100"
    />
    <button
      :disabled="!inputAllowable"
      v-bind:class="classObject"
      class="flex-no-shrink flex-grow w-20 p-2 border-2 rounded"
    >
      Add
    </button>
  </form>
  <p class="mb-8 text-sm text-gray-400">
    Task name length should be
    <span class="font-bold"> more than {{ inputMinLength }}</span> characters,
    currently, you have
    <span class="font-bold">{{ inputLength }}</span> characters.
  </p>
</template>

<script>
export default {
  emits: ["add-task", "AddTask"],
  data() {
    return {
      inputMinLength: 5,
      name: ""
    };
  },
  methods: {
    submitTask() {
      this.$emit("add-task", this.name);
      this.name = "";
    }
  },
  computed: {
    inputLength: function() {
      return this.name.length;
    },
    inputAllowable: function() {
      if (this.inputMinLength - this.inputLength < 0) {
        return true;
      } else {
        return false;
      }
    },
    classObject: function() {
      return {
        "add-active": this.inputAllowable,
        "add-disabled": !this.inputAllowable
      };
    }
  }
};
</script>

<style scoped>
.add-active {
  @apply text-green-600 border-green-600;
}

.add-active:hover {
  @apply text-white bg-green-600;
}

.add-disabled {
  @apply text-gray-300 border-gray-300;
}
</style>
