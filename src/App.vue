<template>
<pre>
{{ patient }}
</pre>

<pre>
{{ validationStatus }}
</pre>
</template>

<script>
import { reactive, computed } from 'vue'
import { patientForm, validatePatient } from './validations.js'

export default {
  setup() {
    const patient = reactive({
      name: '',
      weight: {
        value: 100,
        units: 'kg'
      }
    })

    const validationStatus = computed(() => {
      return validatePatient(patient)
    })

    return {
      patient,
      validationStatus
    }
  }
}
</script>

<style>
</style>
