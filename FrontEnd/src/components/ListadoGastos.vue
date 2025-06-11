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

<style scoped>
.lista-gastos {
  list-style: none;
  padding: 0;
  margin-top: 1.5rem;
}

.item-gasto {
  background: #F3E5AB;
  border-left: 5px solid #A0522D;
  padding: 0.85rem;
  margin-bottom: 0.7rem;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  font-family: 'Segoe UI', sans-serif;
  font-size: 1rem;
  color: #3e2f23;
}

.item-gasto strong {
  color: #7B3F00;
}

.item-gasto em {
  color: #5e503f;
}
</style>