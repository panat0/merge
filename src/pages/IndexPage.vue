<template>
  <div class="q-pa-md" style="max-width: 400px">

    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
      <q-input
        filled
        v-model="id"
        label="รหัสนักศึกษา *"
        hint="รหัสนักศึกษา"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'โปรดใส่รหัสนักศึกษา']"
      />
      <q-input
        filled
        v-model="name"
        label="ชื่อ *"
        hint="ชื่อ"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'โปรดใส่ชื่อ']"
      />
      <q-input
        filled
        v-model="surname"
        label="นามสกุล *"
        hint="นามสกุล"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'โปรดใส่นามสกุล']"
      />
      <q-input
        filled
        v-model="language"
        label="ภาษา *"
        hint="ภาษา"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'โปรดใส่ภาษา']"
      />

      <q-input
        filled
        type="number"
        v-model="age"
        label="อายุ *"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'โปรดใส่อายุ',
          val => val > 0 && val < 100 || 'โปรดใส่อายุ'
        ]"
      />

      <q-toggle v-model="accept" label="ยอมรับเงื่อนไข" />

      <div>
        <q-btn label="Submit" type="submit" color="primary"/>
        <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>

  </div>
</template>

<script>
import { useQuasar } from 'quasar'
import { ref } from 'vue'

export default {
  setup () {
    const $q = useQuasar()

    const id = ref("6604101350")
    const name = ref('ปาณัสม์')
    const surname = ref('บุญเลา')
    const language = ref('ภาษาไทย')
    const age = ref(null)
    const accept = ref(false)

    return {
      id,
      name,
      surname,
      language,
      age,
      accept,

      onSubmit () {
        if (accept.value !== true) {
          $q.notify({
            color: 'red-5',
            textColor: 'white',
            icon: 'warning',
            message: 'You need to accept the license and terms first'
          })
        }
        else {
          $q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            message: 'Submitted'
          })
        }
      },

      onReset () {
        id.value = null
        name.value = null
        surname.value = null
        language.value = null
        age.value = null
        accept.value = false
      }
    }
  }
}
</script>
