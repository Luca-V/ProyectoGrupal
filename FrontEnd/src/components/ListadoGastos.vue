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

<style>
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
</style>