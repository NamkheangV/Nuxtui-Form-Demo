<script setup lang="ts">
import { z } from 'zod'
import type { FormSubmitEvent } from '#ui/types'

const emailSchema = z.object({
  email: z.string().email('Invalid email'),
  password: z.string().min(8, 'Must be at least 8 characters')
})

const nameSchema = z.object({
  firstname: z.string().min(3, 'Must be at least 3 characters'),
  lastname: z.string().min(3, 'Must be at least 3 characters')
})

const state = reactive({
  email: undefined,
  password: undefined,
  firstname: undefined,
  lastname: undefined
})

async function onSubmit(event: FormSubmitEvent<Schema>) {
  console.log('Submit Email success!!', event.data)
}

async function onSubmit2(event: FormSubmitEvent<Schema>) {
  console.log('Hello', event.data)
}
</script>

<template>
  <div class="w-full h-screen flex gap-6 justify-center items-center">
    <div class="h-[20rem] w-[20rem] p-4 rounded-xl border">
      <UForm :schema="emailSchema" :state="state" class="space-y-4" @submit="onSubmit">
        <UFormGroup label="Email" name="email">
          <UInput v-model="state.email" />
        </UFormGroup>

        <UFormGroup label="Password" name="password">
          <UInput v-model="state.password" type="password" />
        </UFormGroup>

        <UButton type="submit">
          Submit
        </UButton>
      </UForm>
    </div>

    <div class="h-[20rem] w-[20rem] p-4 rounded-xl border">
      <UForm :schema="nameSchema" :state="state" class="space-y-4" @submit="onSubmit2">
        <UFormGroup label="Firstname" name="firstname">
          <UInput v-model="state.firstname" />
        </UFormGroup>

        <UFormGroup label="Lastname" name="lastname">
          <UInput v-model="state.lastname"/>
        </UFormGroup>

        <UButton type="submit">
          Submit
        </UButton>
      </UForm>
    </div>
  </div>
</template>

<style></style>