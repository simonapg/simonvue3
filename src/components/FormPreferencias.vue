<template>
  <fieldset>
    <legend>Preferencias</legend>
    
    <div class="form-group">
      <label>Nivel de Experiencia:</label>
      <div class="radio-group">
        <div v-for="nivel in niveles" :key="nivel" class="radio-option">
          <input 
            :id="`nivel-${nivel}`"
            :checked="modelValue.nivel === nivel"
            @change="emitUpdate('nivel', nivel)"
            type="radio"
            :value="nivel"
          />
          <label :for="`nivel-${nivel}`" class="label-inline">{{ nivel }}</label>
        </div>
      </div>
    </div>

    <div class="form-group">
      <label>Intereses (mínimo 1):</label>
      <div class="checkbox-group">
        <div v-for="interes in interesOptions" :key="interes" class="checkbox-option">
          <input 
            :id="`interes-${interes}`"
            :checked="modelValue.intereses.includes(interes)"
            @change="toggleInteres(interes)"
            type="checkbox"
            :value="interes"
          />
          <label :for="`interes-${interes}`" class="label-inline">{{ interes }}</label>
        </div>
      </div>
      <span v-if="errores.intereses" class="error-msg">{{ errores.intereses }}</span>
    </div>

    <div class="form-group">
      <label for="pais">País:</label>
      <select 
        id="pais"
        :value="modelValue.pais?.code || ''"
        @change="cambiarPais"
        class="form-input"
      >
        <option value="" disabled>Selecciona un país</option>
        <option v-for="pais in paises" :key="pais.code" :value="pais.code">
          {{ pais.name }}
        </option>
      </select>
    </div>

    <div class="form-group">
      <label for="tecnologias">Tecnologías (múltiple):</label>
      <!-- Sin :value en select porque se borra la seleccion no permitiendo elegir mas de 2 a la ves (feedback si se puede hacer de otra manera, gracias) -->
      <select 
        id="tecnologias"
        @input="cambiarTecnologias"
        multiple
        class="form-input form-select-multiple"
      >
        <option 
          v-for="tech in tecnologias" 
          :key="tech" 
          :value="tech"
          :selected="modelValue.tecnologias.includes(tech)"
        >
          {{ tech }}
        </option>
      </select>
      <small>Mantén presionado Ctrl (Cmd en Mac) para seleccionar múltiples</small>
    </div>
  </fieldset>
</template>

<script>
export default {
  name: 'FormPreferencias',
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
  data() {
    return {
      niveles: ['junior', 'semi senior', 'senior'],
      interesOptions: ['Frontend', 'Backend', 'DevOps', 'UI/UX', 'Testing'],
      paises: [
        { code: 'CL', name: 'Chile' },
        { code: 'AR', name: 'Argentina' },
        { code: 'MX', name: 'México' },
        { code: 'CO', name: 'Colombia' },
        { code: 'ES', name: 'España' },
        { code: 'US', name: 'Estados Unidos' }
      ],
      tecnologias: ['Vue', 'React', 'Angular', 'Svelte', 'Next.js', 'Nuxt']
    }
  },
  emits: ['update:modelValue'],
  methods: {
    emitUpdate(campo, valor) {
      this.$emit('update:modelValue', {
        ...this.modelValue,
        [campo]: valor
      })
    },
    toggleInteres(interes) {
      const intereses = this.modelValue.intereses.includes(interes)
        ? this.modelValue.intereses.filter(i => i !== interes)
        : [...this.modelValue.intereses, interes]
      this.emitUpdate('intereses', intereses)
    },
    cambiarPais(event) {
      const pais = this.paises.find(p => p.code === event.target.value) || null
      this.emitUpdate('pais', pais)
    },
    cambiarTecnologias(event) {
      const tecnologias = Array.from(event.target.selectedOptions, option => option.value)
      this.emitUpdate('tecnologias', tecnologias)
    }
  }
}
</script>

<style scoped>
</style>
