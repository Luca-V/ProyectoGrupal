<script setup>
import { ref } from "vue";

const gastos = ref([]);

const obtenerGastos = async () => {
  const res = await fetch("http://localhost:5297/api/Gastos", {
    method: "GET",
    headers: { "Content-Type": "application/json" },
  });

  const gastosObtenidos = await res.json();

  gastos.value = gastosObtenidos;
};

obtenerGastos();
</script>

<template>
  <ul class="lista-gastos">
    <li v-for="gasto in gastos" :key="gasto.id" class="item-gasto">
      <strong>{{ gasto.descripcion }}</strong>
      - ${{ gasto.monto.toFixed(2) }} en <em>{{ gasto.nombreComercio }}</em> ({{
        gasto.fecha.slice(0, 10)
      }})
    </li>
  </ul>
</template>

<!---------<style>
h1 {
  text-align: center;
  color: #333;
  margin-bottom: 1.5rem;
}

h2 {
  color: #444;
  margin-bottom: 1rem;
}

.lista-gastos {
  list-style: none;
  padding: 0;
}

.item-gasto {
  background: #fff;
  border-left: 4px solid #0077cc;
  padding: 0.75rem;
  margin-bottom: 0.5rem;
  border-radius: 8px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
}
</style>------>
<style scoped>
.lista-gastos {
  list-style: none;
  padding: 0;
  margin-top: 1.5rem;
}

.item-gasto {
  background: #F3E5AB; /* vainilla */
  border-left: 5px solid #A0522D; /* terracota */
  padding: 0.85rem;
  margin-bottom: 0.7rem;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  font-family: 'Segoe UI', sans-serif;
  font-size: 1rem;
  color: #3e2f23; /* marrón suave */
}

.item-gasto strong {
  color: #7B3F00; /* más oscuro */
}

.item-gasto em {
  color: #5e503f;
}
</style>

