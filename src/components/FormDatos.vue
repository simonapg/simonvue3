<template>
  <fieldset>
    <legend>Datos Básicos</legend>
    
    <div class="form-group">
      <label for="nombre">Nombre (requerido):</label>
      <input 
        id="nombre"
        v-model.trim="datos.nombre"
        type="text"
        placeholder="Ingresa tu nombre"
        class="form-input"
        :class="{ 'error': errores.nombre }"
        @input="actualizar"
      />
      <span v-if="errores.nombre" class="error-msg">{{ errores.nombre }}</span>
    </div>

    <div class="form-group">
      <label for="edad">Edad (0-120):</label>
      <input 
        id="edad"
        v-model.number="datos.edad"
        type="number"
        min="0"
        max="120"
        class="form-input"
        :class="{ 'error': errores.edad }"
        @input="actualizar"
      />
      <span v-if="errores.edad" class="error-msg">{{ errores.edad }}</span>
    </div>

    <div class="form-group">
      <label for="biografia">Biografía:</label>
      <textarea 
        id="biografia"
        v-model.lazy="datos.biografia"
        placeholder="Cuéntanos sobre ti..."
        rows="4"
        class="form-input"
        maxlength="200"
        @change="actualizar"
      ></textarea>
      <small>{{ datos.biografia.length }} / 200 caracteres</small>
    </div>
  </fieldset>
</template>

<script>
export default {
  name: 'FormDatos',
  props: {
    modelValue: {
      type: Object,
      required: true
    },
    errores: {
      type: Object,
      required: true
    }
  },
  emits: ['update:modelValue'],
  data() {
    return {
      datos: { ...this.modelValue }
    }
  },
  watch: {
    modelValue: {
      handler(newVal) {
        this.datos = { ...newVal }
      },
      deep: true
    }
  },
  methods: {
    actualizar() {
      this.$emit('update:modelValue', this.datos)
    }
  }
}
</script>

<style scoped>
</style>
