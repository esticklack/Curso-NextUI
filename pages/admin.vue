<template>
  <div>
    <h1>Ruta protegida</h1>
    <UButton @click="logout">Salir</UButton>
  </div>
</template>

<script lang="ts" setup>

  const {logout} = useFirebaseAuth();

</script>


<style>

</style>