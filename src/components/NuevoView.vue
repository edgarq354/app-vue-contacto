<template>
 
    <div class="container mt-4"> 

    <form @submit.prevent="submit" novalidate>
      <div class="mb-3">
        <label class="form-label">Nombre</label>
        <input v-model="contacto.name" type="text" class="form-control" :class="{'is-invalid': v$.contacto.name.$error}" />
        <div class="invalid-feedback">Nombre es obligatoria</div>
      </div>

      <div class="mb-3">
        <label class="form-label">Correo Electrónico</label>
        <input v-model="contacto.email" type="email" class="form-control" :class="{'is-invalid': v$.contacto.email.$error}" />
        <div class="invalid-feedback">Correo Electrónico es obligatorio</div>
      </div>

      <div class="mb-3">
        <label class="form-label">Dirección</label>
        <input v-model="contacto.address" type="text" class="form-control" :class="{'is-invalid': v$.contacto.address.$error}" />
        <div class="invalid-feedback">Dirección es obligatorio</div>
      </div>

      <div class="mb-3">
        <label class="form-label">Telefono</label>
        <input v-model="contacto.phone" type="number" class="form-control" :class="{'is-invalid': v$.contacto.phone.$error}" />
        <div class="invalid-feedback">Telefono debe ser numero</div>
      </div>

      <div class="mb-3">
        <label class="form-label">País</label>
        <input v-model="contacto.country" type="text"   class="form-control" :class="{'is-invalid': v$.contacto.country.$error}" />
        <div class="invalid-feedback">País es obligatorio</div>
      </div>
      <div class="mb-3">
        <label class="form-label">Ciudad</label>
        <input v-model="contacto.city" type="text"   class="form-control" :class="{'is-invalid': v$.contacto.city.$error}" />
        <div class="invalid-feedback">Ciudad  es obligatorio</div>
      </div>
   

      <button type="submit" class="btn btn-primary">Guardar</button>
    </form>
  </div>
  
</template>

<script>
import { reactive } from 'vue'
import useVuelidate from '@vuelidate/core'
import { required, minValue, maxValue, url, email } from '@vuelidate/validators'
export default {
    name: 'NuevoContactoView',
    data() {
        return {
            title: ' Nuevo Contacto',
            contacto: reactive({
                name: '',
                email: '',
                address: '',
                phone: '',
                country: '',
                city: '' 
            }),
            v$: null
        }
    },
    components: {
        // Registro de componentes que se utilizaran.
    },
    created() {
        const currentTelefono = 80000000
        const rules = {
            contacto: {
                name: { required },
                email: { required,email },
                address: { required },
                phone: { required },
                country: { required },
                city: { required } 
            }
        }
        this.v$ = useVuelidate(rules, { contacto: this.contacto })
    },
    methods: {
        // métodos que se pueden llamar desde la plantilla o desde otras partes del componente.
        async submit() {
            const isValid = await this.v$.$validate()
            if (!isValid) {
                alert('Por favor complete correctamente el formulario.')
                return
            }
            this.$emit('created', { ...this.contacto });
        }
    },
    computed: {
        // propiedades computadas que dependen de otras propiedades reactivas
    },
    props: {
        // propiedades que el componente puede recibir.
    },
    emits: [] // los eventos personalizados que el componente puede emitir.
}
</script>

<style></style>