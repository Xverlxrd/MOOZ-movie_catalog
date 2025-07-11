<template>
  <header class="header">
    <img class="header_logo" src="@assets/Logo.jpg" alt="Logo">
    <div class="header_input">
      <Input
          v-model="searchTerm"
          @input="handleInputWithDebounce"
      />
    </div>
    <div class="header_user">
      <img
          src="@assets/User.png"
          alt="UserImg"
          class="header_user_img"
      />
      <p class="header_user_name">Your name</p>
    </div>
  </header>
</template>

<script setup lang="ts">
import Input from "@components/ui/Input/Input.vue";
import {onBeforeUnmount, ref} from "vue";

const emit = defineEmits(['inputWithDebounce'])

const searchTerm = ref('');
let taimerId: ReturnType<typeof setTimeout>;

const handleInputWithDebounce = () => {
  taimerId = setTimeout(() => {
    emit('inputWithDebounce', searchTerm.value)
  }, 1000)

}

onBeforeUnmount(() => {
  clearTimeout(taimerId);
});

</script>

<style scoped lang="scss">
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 47px 0;

  &_user {
    display: flex;
    align-items: center;
    gap: 9px;

    &_name {
      font-weight: 400;
      font-size: 14px;
      line-height: 140%;
    }
  }
}

@media (max-width: 700px) {
  .header {
    flex-direction: column;
    gap: 20px;

    &_input {
      order: 3;
    }
    &_user {
      order: 2;
    }
    &_logo {
      order: 1;
      align-self: start;
    }
  }
}
</style>