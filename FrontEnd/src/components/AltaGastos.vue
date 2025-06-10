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

  const datosGastos = {
    monto: nuevoGasto.value.monto,
    descripcion: nuevoGasto.value.descripcion,
    fecha: nuevoGasto.value.fecha,
    nombreComercio: nuevoGasto.value.nombreComercio
  }

  if (datosGastos.monto <= 0) {
    alert('El monto debe ser mayor a cero')
    return
  }

  if (datosGastos.descripcion.length < 3 || datosGastos.descripcion.length > 250) {
    alert('La descripción debe tener entre 3 y 250 caracteres')
    return
  }

  const formattedDate = new Date().toISOString().split('T')[0]

  if (datosGastos.fecha == "" || datosGastos.fecha <= formattedDate) {
    alert('La fecha debe ser una fecha futura')
    return
  }

  if (datosGastos.nombreComercio.length === 0 || datosGastos.nombreComercio.length > 250) {
    alert('El nombre del comercio no puede estar vacío y debe tener hasta 250 caracteres')
    return
  }

  try {
    await fetch('http://localhost:5297/api/Gastos', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(datosGastos)
    })
    nuevoGasto.value = { monto: 0, descripcion: '', fecha: '', nombreComercio: '' }
    window.location.href = "/ListadoGastos"
  } catch (error) {
    console.log(error)
  }
}
</script>

<template>
    <form @submit="enviarGasto" class="formulario">
      <input name="monto" v-model="nuevoGasto.monto" type="number" placeholder="Monto" step="0.01" />
      <input name="descripcion" v-model="nuevoGasto.descripcion" type="text" placeholder="Descripción" />
      <input name="fecha" v-model="nuevoGasto.fecha" type="date" />
      <input name="nombreComercio" v-model="nuevoGasto.nombreComercio" type="text" placeholder="Nombre del comercio" />
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

