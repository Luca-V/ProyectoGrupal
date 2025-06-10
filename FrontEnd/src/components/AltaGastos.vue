<script setup>
import { ref } from 'vue'

const nuevoGasto = ref({
  monto: 0,
  descripcion: '',
  fecha: '',
  nombreComercio: ''
})

const enviarGasto = async (e) => {
  e.preventDefault()
  await fetch('http://localhost:5297/api/Gastos', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(nuevoGasto.value)
  })
  nuevoGasto.value = { monto: 0, descripcion: '', fecha: '', nombreComercio: '' }

  window.location.href = "/ListadoGastos"
}
</script>

<template>
    <form @submit="enviarGasto" class="formulario">
      <input v-model="nuevoGasto.monto" placeholder="Monto" type="number" step="0.01" required />
      <input v-model="nuevoGasto.descripcion" placeholder="Descripción" required />
      <input v-model="nuevoGasto.fecha" type="date" required />
      <input v-model="nuevoGasto.nombreComercio" placeholder="Nombre del comercio" required />
      <button type="submit">Agregar Gasto</button>
    </form>
</template>

<!--------<style>
.formulario {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 2rem;
}

.formulario input {
  padding: 0.7rem;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 1rem;
}

.formulario button {
  padding: 0.7rem;
  background-color: #0077cc;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.formulario button:hover {
  background-color: #005fa3;
}
</style>------->
<style scoped>
.formulario {
  background-color: #C19A6B; /* camel */
  padding: 2rem;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  gap: 1rem;
  color: #333;
}

.formulario input {
  background-color: #F3E5AB; /* vainilla */
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 0.75rem;
  font-size: 1rem;
  color: #333;
  transition: border 0.3s, box-shadow 0.3s;
}

.formulario input:focus {
  border-color: #A0522D;
  box-shadow: 0 0 5px rgba(160, 82, 45, 0.3);
  outline: none;
}

.formulario button {
  padding: 0.75rem;
  background-color: #A0522D; /* terracota */
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.formulario button:hover {
  background-color: #7B3F00;
}
</style>

