/* eslint-disable no-useless-escape */ /* eslint-disable no-useless-escape */
<template>
  <form @submit.prevent="onSubmit">
    <BaseInput label="Email" type="email" v-model="email" :error="emailError" />

    <BaseInput label="Password" type="password" />

    <BaseButton type="submit" class="-fill-gradient"> Submit </BaseButton>
  </form>
</template>

<script>
import { useField } from 'vee-validate'
export default {
  setup() {
    function onSubmit() {
      alert('Submitted')
    }
    const { value: email, errorMessage: emailError } = useField(
      'email',
      (value) => {
        if (!value) return 'This field is required'
        const regex = /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/
        if (!regex.test(String(value).toLowerCase())) {
          return 'Please enter a valid email address'
        }
        return true
      }
    )

    return {
      onSubmit,
      email: email,
      emailError: emailError,
    }
  },
}
</script>
