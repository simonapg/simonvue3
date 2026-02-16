<template>
  <div class="resumen-container">
    <h2>Resumen en Tiempo Real</h2>
    <div class="resumen-content">
      <div class="resumen-item">
        <strong>Nombre:</strong> {{ formulario.nombre || '(no ingresado)' }}
      </div>
      <div class="resumen-item">
        <strong>Edad:</strong> {{ formulario.edad || '(no especificada)' }}
      </div>
      <div class="resumen-item">
        <strong>Biografía:</strong> {{ formulario.biografia || '(vacía)' }}
      </div>
      <div class="resumen-item">
        <strong>Nivel:</strong> {{ formulario.nivel || '(no seleccionado)' }}
      </div>
      <div class="resumen-item">
        <strong>Intereses:</strong> 
        <span v-if="formulario.intereses.length > 0">{{ formulario.intereses.join(', ') }}</span>
        <span v-else>(ninguno seleccionado)</span>
      </div>
      <div class="resumen-item">
        <strong>País:</strong> 
        <span v-if="formulario.pais">{{ formulario.pais.name }} ({{ formulario.pais.code }})</span>
        <span v-else>(no seleccionado)</span>
      </div>
      <div class="resumen-item">
        <strong>Tecnologías:</strong>
        <span v-if="formulario.tecnologias.length > 0">{{ formulario.tecnologias.join(', ') }}</span>
        <span v-else>(ninguna seleccionada)</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ResumenFormulario',
  props: {
    formulario: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.resumen-container {
  background: #fff;
  padding: 30px 0;
  border-bottom: 1px solid #000;
  border-left: none;
  box-shadow: none;
  position: static;
  top: auto;
  max-height: none;
  overflow-y: visible;
}

.resumen-container h2 {
  border-bottom: none;
  border-top: 1px solid #000;
  padding-top: 30px;
  padding-bottom: 20px;
  margin-bottom: 20px;
}

.resumen-content {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.resumen-item {
  padding: 0;
  background: transparent;
  border-radius: 0;
  border-left: none;
  font-size: 14px;
  line-height: 1.6;
  color: #000;
  border-bottom: 1px solid #eee;
  padding-bottom: 12px;
}

.resumen-item strong {
  color: #000;
  display: inline-block;
  min-width: 120px;
  font-weight: 500;
}

@media (max-width: 768px) {
  .resumen-container {
    border-bottom: 1px solid #000;
  }
}
</style>
