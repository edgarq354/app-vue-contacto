<template>
    <div class="container mt-4"> 
  
      <form @submit.prevent="emitirDatosEditados" novalidate>
        <div class="mb-3">
          <label class="form-label">Nombre</label>
          <input v-model="editado.name" type="text" class="form-control" required />
        </div>
  
        <div class="mb-3">
          <label class="form-label">Correo Electrónico</label>
          <input v-model.email="editado.email" type="email" class="form-control" required />
        </div>
  
        <div class="mb-3">
          <label class="form-label">Dirección</label>
          <input v-model="editado.address" type="text" class="form-control" required />
        </div>
  
        <div class="mb-3">
          <label class="form-label">Telefono</label>
          <input v-model="editado.phone" type="text" class="form-control" required />
        </div>
  
        <div class="mb-3">
          <label class="form-label">País</label>
          <input v-model="editado.country" type="text"   class="form-control" required />
        </div>

        <div class="mb-3">
          <label class="form-label">Ciudad</label>
          <input v-model="editado.city" type="text"   class="form-control" required />
        </div>
  
        <button type="submit" class="btn btn-success">Guardar Cambios</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ContactoEditor',
    props: {
      auto: {
        type: Object,
        required: true
      }
    },
    data() {
      return {
        // Copia del objeto original para evitar modificarlo directamente
        editado: { ...this.auto }
      }
    },
    methods: {
      emitirDatosEditados() {
        // Emitimos un evento con los datos modificados
        this.$emit('update', this.editado)
      }
    }
  }
  </script>
  