<template>
  <form @submit.prevent="onSubmit">
    <BaseInput label="Email" type="email" :modelValue="email" :error="emailError" @change="handleChange" />

    <BaseInput label="Password" type="password" v-model="password" :error="passwordError" />

    <BaseButton type="submit" class="-fill-gradient"> Submit </BaseButton>
  </form>
</template>

<script>
import { useField, useForm } from 'vee-validate'
export default {
  setup() {
    function onSubmit() {
      alert('Submitted')
    }

    const validations = {
      email: (value) => {
        if (!value) return 'This field is required'
        const regex = /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/
        if (!regex.test(String(value).toLowerCase())) {
          return 'Please enter a valid email address'
        }
        return true
      },
      password: (value) => {
        const requiredMessage = 'This field is required'
        if (value === undefined || value === null) return requiredMessage
        if (!String(value).length) return requiredMessage
        return true
      },
    }

    const { setFieldValue } = useForm({ validationSchema: validations })
    const { value: email, errorMessage: emailError } = useField('email')
    const { value: password, errorMessage: passwordError } = useField('password')
    const handleChange = (event) => {
      setFieldValue('email', event.target.value)
    }

    return {
      onSubmit,
      email: email,
      emailError: emailError,
      password,
      passwordError,
      handleChange,
    }
  },
}
</script>
