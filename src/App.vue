<template>
  <div id="app" class="container">
    <h1>Formulario de Registro / Perfil</h1>
    
    <form @submit.prevent="enviarFormulario" class="form-container">
      <FormDatos 
        :modelValue="formulario"
        :errores="errores"
        @update:modelValue="formulario = $event"
      />

      <FormPreferencias 
        :modelValue="formulario"
        :errores="errores"
        @update:modelValue="formulario = $event"
      />

      <button 
        type="submit" 
        class="btn btn-submit"
        :disabled="!formularioValido"
      >
        Enviar Formulario
      </button>
    </form>

    <ResumenFormulario :formulario="formulario" />

    <ModalConfirmacion 
      :mostrar="mostrarModal"
      :datosEnviados="datosEnviados"
      @cerrar="cerrarModal"
    />
  </div>
</template>

<script>
import FormDatos from './components/FormDatos.vue'
import FormPreferencias from './components/FormPreferencias.vue'
import ResumenFormulario from './components/ResumenFormulario.vue'
import ModalConfirmacion from './components/ModalConfirmacion.vue'

export default {
  name: 'App',
  components: {
    FormDatos,
    FormPreferencias,
    ResumenFormulario,
    ModalConfirmacion
  },
  data() {
    return {
      formulario: {
        nombre: '',
        edad: null,
        biografia: '',
        nivel: '',
        intereses: [],
        pais: null,
        tecnologias: []
      },
      errores: {
        nombre: '',
        edad: '',
        intereses: ''
      },
      mostrarModal: false,
      datosEnviados: ''
    }
  },
  computed: {
    formularioValido() {
      return (
        this.formulario.nombre.length > 0 &&
        this.formulario.edad !== null &&
        this.formulario.edad >= 0 &&
        this.formulario.edad <= 120 &&
        this.formulario.intereses.length > 0
      )
    }
  },
  methods: {
    validarFormulario() {
  
      this.errores.nombre = ''
      this.errores.edad = ''
      this.errores.intereses = ''

     
      if (!this.formulario.nombre) {
        this.errores.nombre = 'El nombre es requerido'
      }

     
      if (this.formulario.edad === null || this.formulario.edad < 0 || this.formulario.edad > 120) {
        this.errores.edad = 'La edad debe estar entre 0 y 120'
      }

     
      if (this.formulario.intereses.length === 0) {
        this.errores.intereses = 'Debes seleccionar al menos un interés'
      }

      return this.formularioValido
    },
    enviarFormulario() {
      if (!this.validarFormulario()) {
        alert('Por favor, corrige los errores del formulario')
        return
      }

      this.datosEnviados = JSON.stringify(this.formulario, null, 2)
      console.log('Datos del formulario enviados:', this.formulario)
      this.mostrarModal = true
    },
    cerrarModal() {
      this.mostrarModal = false
    }
  }
}
</script>

<style scoped>
#app {
  padding: 40px 20px;
  max-width: 900px;
  margin: 0 auto;
}

.container {
  display: flex;
  flex-direction: column;
  gap: 40px;
}

h1 {
  text-align: center;
  margin: 0 0 30px 0;
}

.form-container {
  background: #fff;
  padding: 0;
  border-radius: 0;
  box-shadow: none;
  border-bottom: 1px solid #000;
}

.btn-submit {
  width: 100%;
  margin-top: 30px;
}

@media (max-width: 768px) {
  #app {
    padding: 20px 15px;
  }
}
</style>
