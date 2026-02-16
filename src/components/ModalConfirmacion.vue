<template>
  <div v-if="mostrar" class="modal-overlay" @click="cerrar">
    <div class="modal" @click.stop>
      <h3>¡Formulario Enviado Correctamente!</h3>
      <p>Los datos han sido procesados exitosamente.</p>
      <pre class="json-output">{{ datosEnviados }}</pre>
      <button @click="cerrar" class="btn btn-close">Cerrar</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModalConfirmacion',
  props: {
    mostrar: {
      type: Boolean,
      required: true
    },
    datosEnviados: {
      type: String,
      required: true
    }
  },
  emits: ['cerrar'],
  methods: {
    cerrar() {
      this.$emit('cerrar')
    }
  }
}
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal {
  background: white;
  border-radius: 0;
  padding: 40px;
  max-width: 500px;
  width: 90%;
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.2);
  max-height: 80vh;
  overflow-y: auto;
  border: 1px solid #000;
}

.modal h3 {
  margin-bottom: 15px;
}

.modal p {
  color: #666;
  margin-bottom: 20px;
  font-size: 14px;
}

.json-output {
  background: #f5f5f5;
  color: #000;
  padding: 15px;
  border-radius: 0;
  border: 1px solid #ddd;
  overflow-x: auto;
  max-height: 300px;
  font-size: 12px;
  margin: 20px 0;
  font-family: 'Courier New', monospace;
}

.btn-close {
  width: 100%;
  margin-top: 20px;
}
</style>
