<template>
  <div class="loader-container">
    <div class="loader"></div>
  </div>
</template>

<style scoped lang="scss">
.loader-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 200px;
}

.loader {
  width: 48px;
  height: 48px;
  border: 5px solid #f3f3f3;
  border-top: 5px solid #3256E3;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>