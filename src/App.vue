<template>
  <form>
    <div class="field">
      <div class="error" v-if="!validationStatus.name.valid">
        {{ validationStatus.name.message }}
      </div>
      <label for="name">Name</label>
      <input type="text" id="name" v-model="patient.name">
    </div>

    <div class="field">
      <div class="error" v-if="!validationStatus.weight.valid">
        {{ validationStatus.weight.message }}
      </div>
      <label for="weight">Weight</label>
      <input type="text" id="weight" v-model.number="patient.weight.value">
      <select v-model="patient.weight.units">
        <option value="kg">kg</option>
        <option value="lb">lb</option>
      </select>
    </div>

    <button type="submit" :disabled="!formValid">Submit</button>
  </form>
<pre>
{{ patient }}
</pre>

<pre>
{{ validationStatus }}
{{ formValid }}
</pre>
</template>

<script>
import { reactive, computed } from 'vue'
import { patientForm, validatePatient, isFormValid } from './validations.js'

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

    const formValid = computed(() => {
      return isFormValid(validationStatus.value)
    })

    return {
      patient,
      formValid,
      validationStatus
    }
  }
}
</script>

<style>
.field > label {
  display: inline-block;
  width: 50px;
  margin: 0 0 20px 0;
}
.field > input {
  display: inline-block;
  margin: 2px;
}
.error {
  color: red;
}
</style>
