<template>
  <q-page class="flex column q-pa-md">
    <q-file
      v-model="selectedImg"
      :filter="checkFileType"
      :rules="formRules.img"
      ref="imgRef"
      lazy-rules="ondemand"
      label="Выберите изображение"
      accept="image/*"
      class="full-width"
      color="primary"
      filled
      counter
      clearable
      @update:model-value="onChange"
    >
      <template v-slot:prepend>
        <q-icon name="folder_open" />
      </template>

      <template v-slot:after>
        <q-btn
          color="primary"
          icon="send"
          flat
          @click="onSubmit"
        />
      </template>
    </q-file>

    <div class="flex justify-center q-my-md">
      <q-img
        :src="previewUrl"
        spinner-color="white"
        fit
        class="rounded-borders"
        style="height: 400px; max-width: 600px;"
      >
        <div
          v-if="recognitionResult"
          class="absolute-bottom text-subtitle1 text-center"
        >
          {{ recognitionResult }}
        </div>
      </q-img>
    </div>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'
import { useQuasar } from 'quasar'

const $q = useQuasar()

const formRules = {
  img: [v => !!v || 'Файл не выбран']
}

const imgRef = ref(null)

const selectedImg = ref(null)
const previewUrl = ref('')

const recognitionResult = ref('')

const onChange = file => {
  previewUrl.value = file ? URL.createObjectURL(file) : ''
  recognitionResult.value = ''
  imgRef.value.resetValidation()
}

const onSubmit = async () => {
  const isValid = await imgRef.value.validate()
  if (!isValid) { return }

  $q.loading.show({
    message: 'Идет распознавание...'
  })

  const formData = new FormData()
  formData.append('img', selectedImg.value)

  try {
    const response = await fetch(process.env.API_URL + '/recognize', {
      method: 'POST',
      body: formData,
    })
    const { result } = await response.json()
    recognitionResult.value = result
  } catch (error) {
    $q.notify('Произошла ошибка распознавания')
  } finally {
    $q.loading.hide()
  }
}
</script>
