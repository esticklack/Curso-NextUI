<script setup lang="ts">
import { z } from 'zod'
import type { FormSubmitEvent } from '#ui/types'

const {register} = useFirebaseAuth()

//Datos reactivos, estarán pendientes del HTML y se van a hacer una renderización
//const email = ref('');
//const password = ref('');

const schema = z.object({
  email: z.string().email('Invalid email'),
  password: z.string().min(6, 'Must be at least 6 characters')
})

type Schema = z.output<typeof schema>

const state = reactive({
  email: undefined,
  password: undefined
})

async function onSubmit (event: FormSubmitEvent<Schema>) {
  // Do something with data
  console.log(event.data)
  try {
    await register(event.data.email, event.data.password);
  } catch (error) {
    console.log(error)
  }
}

</script>

<template>
    <UForm :schema="schema" :state="state" class="space-y-4" @submit="onSubmit">
      <UFormGroup label="Email" name="email" class="mb-4">
        <UInput v-model.trim="state.email" />
      </UFormGroup>
  
      <UFormGroup label="Password" name="password" class="mb-4">
        <UInput v-model.trim="state.password" type="password" />
      </UFormGroup>
  
      <UButton type="submit" class="">
        Submit
      </UButton>
    </UForm>
  </template>