<template>
  <section class="hero">
    <div class="container">
      <h2>Encuentra el auto perfecto para ti</h2>
      <p>Autos nuevos y seminuevos con garantía y el mejor precio del mercado.</p>
      <a href="/catalogo" class="btn">Ver catálogo</a>
    </div>
  </section>

  
  <section id="beneficios" class="beneficios">
    <div class="container">
      <h3>¿Por qué elegirnos?</h3>
      <ul>
        <li>✔️ Garantía extendida en todos los autos</li>
        <li>✔️ Financiación a medida</li>
        <li>✔️ Revisión mecánica certificada</li>
        <li>✔️ Asesoría personalizada</li>
      </ul>
    </div>
  </section>

  <section id="testimonios" class="testimonios">
    <div class="container">
      <h3>Lo que dicen nuestros clientes</h3>
      <blockquote>
        "Excelente servicio, compré mi auto en línea y fue todo muy claro. 100% recomendados."
        <cite>- Juan Pérez</cite>
      </blockquote>
      <blockquote>
        "La atención fue increíble, y me ofrecieron mejores condiciones que el concesionario."
        <cite>- Ana López</cite>
      </blockquote>
    </div>
  </section>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  }
}
</script>


<style>

.hero {
  background: #eee;
  text-align: center;
  padding: 4rem 1rem;
}

.hero h2 {
  font-size: 2rem;
  margin-bottom: 1rem;
}

.hero .btn {
  display: inline-block;
  background: #000;
  color: #fff;
  padding: 0.8rem 1.5rem;
  text-decoration: none;
  margin-top: 1rem;
  border-radius: 5px;
}



/* Beneficios */
.beneficios ul {
  list-style: none;
  padding: 1rem 0;
}

.beneficios li {
  margin-bottom: 0.5rem;
}

/* Testimonios */
.testimonios blockquote {
  background: #f9f9f9;
  padding: 1rem;
  margin: 1rem 0;
  border-left: 5px solid #ccc;
}

/* Footer */
footer {
  background: #f0f0f0;
  text-align: center;
  padding: 2rem 1rem;
  font-size: 0.9rem;
}

/* ====== RESPONSIVE ====== */
@media (max-width: 768px) {

  .hero h2 {
    font-size: 1.5rem;
  }

  .autos .grid {
    flex-direction: column;
  }

  .card {
    flex: 1 1 100%;
  }

  .beneficios ul {
    padding-left: 1rem;
  }

  .testimonios blockquote {
    font-size: 0.95rem;
  }
}
</style>