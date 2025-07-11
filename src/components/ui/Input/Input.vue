<template>
  <div class="wrapper">
    <input
        :placeholder="placeholder"
        :value="modelValue"
        @input="$emit('update:modelValue', ($event.target as HTMLInputElement).value)"
        @keyup.enter="$emit('search', modelValue)"
        :type="type"
        class="input"
    />
    <span v-if="type === 'text'" class="input-icon">
      <img src="@/assets/Search.png" alt="Search"/>
    </span>
  </div>
</template>

<script setup lang="ts">
defineProps({
  placeholder: {
    type: String,
    default: 'Search...'
  },
  modelValue: {
    type: String,
    default: ''
  },
  type: {
    type: String,
    default: 'text'
  }
});

defineEmits(['update:modelValue', 'search'])
</script>

<style scoped>
.wrapper {
  position: relative;
  width: 100%;
  height: 40px;
  max-width: 280px;
}
.input {
  width: 85%;
  padding: 10px 40px 10px 15px;
  border: 1px solid #E6EAF5;
  border-radius: 5px;
  background: #FCFCFF;
  transition: border-color 0.3s ease;
  font-size: 14px;
  color: #929BBC;


  &:focus {
    outline: none;
  }
}

.input-icon {
  position: absolute;
  right: 0;
  top: 55%;
  transform: translateY(-50%);
  color: #999;
  pointer-events: none;

  img {
    width: 16px;
    height: 16px;
  }
}
</style>