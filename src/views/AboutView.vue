<template>
  <section class="about">
    <div class="container">
      <div class="about-text">
        <h2>Acerca del Sistema de Autoventa</h2>
        <p>
          Este proyecto es un ejemplo de un sistema de autoventa desarrollado como parte del
          <strong>Diplomado Full Stack</strong> de la
          <strong>Universidad Simón I. Patiño</strong>.
        </p>
        <p>
          El sistema permite gestionar la venta de automóviles nuevos y usados, integrando funcionalidades como:
          registro de vehículos, catálogo interactivo, gestión de usuarios y procesos de compra.
        </p>
        <p>
          Ha sido creado como una aplicación práctica para demostrar habilidades adquiridas en desarrollo
          web frontend y backend, bases de datos, APIs REST y despliegue web.
        </p>
      </div>

    </div>
  </section>
</template>

<script>

export default {
  name: 'AboutView',
  data() {
    return {
      message: 'Hola Mundo'
    }
  },
  components: {
    // Registro de componentes que se utilizaran.
  },
  methods: {
    // métodos que se pueden llamar desde la plantilla o desde otras partes del componente.
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


<style>
.about {
  background-color: #fff;
  padding: 3rem 1rem;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
}

.about-text {
  flex: 1 1 500px;
}

.about-text h2 {
  font-size: 2rem;
  margin-bottom: 1rem;
  color: #2c3e50;
}

.about-text p {
  margin-bottom: 1rem;
  line-height: 1.6;
}

.about-image {
  flex: 1 1 400px;
  text-align: center;
}

.about-image img {
  width: 100%;
  max-width: 500px;
  height: auto;
  border-radius: 8px;
}

/* Responsive */
@media (max-width: 768px) {
  .container {
    flex-direction: column;
    text-align: center;
  }

  .about-text,
  .about-image {
    flex: 1 1 100%;
  }

  .about-text h2 {
    font-size: 1.7rem;
  }
}
</style>