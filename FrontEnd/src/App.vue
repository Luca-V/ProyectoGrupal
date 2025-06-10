<template>
  <main class="container">
    <RouterLink to="/">Inicio</RouterLink>
    <br>
    <RouterLink to="/ListadoGastos">Listado de Gastos</RouterLink>
    <br>
    <RouterLink to="/AltaGastos">Alta de Gastos</RouterLink>

    <RouterView />
  </main>
</template>

<style scoped>
.container {
  max-width: 700px;
  margin: 2rem auto;
  padding: 1.5rem;
  background: #C19A6B; /* camel */
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  color: #3e2f23;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #FFF8E7; /* vainilla clara */
  margin: 0;
  padding: 2rem;
}
</style>

