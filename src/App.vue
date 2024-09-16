<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  setup() {
    const nombre = ref('');
    const apellidos = ref('');
    const edad = ref(0);
    const genero = ref('');
    const correo = ref('');
    const contrasena = ref('');
    const telefono = ref(0);
    const datos = ref<any[]>([]);
    const errorname = ref('');
    const errorapellidos = ref('');
    const erroredad = ref('');
    const errorgenero = ref('');
    const errorcorreo = ref('');
    const errorcontrasena = ref('');
    const errortelefono = ref('');

    const clean = () => {
      nombre.value = '';
      apellidos.value = '';
      edad.value = 0;
      genero.value = '';
      correo.value = '';
      contrasena.value = '';
      telefono.value = 0;
      errorname.value = '';
      errorapellidos.value = '';
      erroredad.value = '';
      errorgenero.value = '';
      errorcorreo.value = '';
      errorcontrasena.value = '';
      errortelefono.value = '';
    };

    // Validación para solo letras
    const isOnlyLetters = (text: string) => /^[a-zA-Z\s]+$/.test(text);

    const valida = () => {
      let valido = true;
      if (!isOnlyLetters(nombre.value)) {
        errorname.value = 'El nombre solo puede contener letras';
        valido = false;
      } else {
        errorname.value = '';
      }

      if (!isOnlyLetters(apellidos.value)) {
        errorapellidos.value = 'Los apellidos solo pueden contener letras';
        valido = false;
      } else {
        errorapellidos.value = '';
      }

      if (edad.value === 0) {
        erroredad.value = 'La edad no puede estar vacía';
        valido = false;
      } else {
        erroredad.value = '';
      }

      if (genero.value === '') {
        errorgenero.value = 'El género no puede estar vacío';
        valido = false;
      }

      if (correo.value === '') {
        errorcorreo.value = 'El correo no puede estar vacío';
        valido = false;
      }

      if (contrasena.value === '') {
        errorcontrasena.value = 'La contraseña no puede estar vacía';
        valido = false;
      }

      if (telefono.value === 0) {
        errortelefono.value = 'El teléfono no puede estar vacío';
        valido = false;
      }

      return valido;
    };

    const guardar = () => {
      if (valida()) {
        datos.value.push({
          nombre: nombre.value,
          apellidos: apellidos.value,
          edad: edad.value,
          genero: genero.value,
          correo: correo.value,
          contrasena: contrasena.value,
          telefono: telefono.value
        });
        clean();
      }
    };

    return {
      nombre,
      apellidos,
      edad,
      genero,
      correo,
      contrasena,
      telefono,
      datos,
      errorname,
      errorapellidos,
      erroredad,
      errorgenero,
      errorcorreo,
      errorcontrasena,
      errortelefono,
      clean,
      valida,
      guardar
    };
  }
});
</script>

<template>
  <div class="main-container">
    <div class="form-container">
      <form>
        <label for="name">Nombre</label>
        <input type="text" id="name" v-model="nombre" placeholder="Introduce tu nombre">
        <span class="error">{{ errorname }}</span>

        <label for="apellidos">Apellidos</label>
        <input type="text" id="apellidos" v-model="apellidos" placeholder="Introduce tus apellidos">
        <span class="error">{{ errorapellidos }}</span>

        <label for="edad">Edad</label>
        <input type="number" id="edad" v-model="edad" placeholder="Introduce tu edad">
        <span class="error">{{ erroredad }}</span>

        <label for="genero">Género</label>
        <input type="text" id="genero" v-model="genero" placeholder="Introduce tu género">
        <span class="error">{{ errorgenero }}</span>

        <label for="correo">Correo</label>
        <input type="email" id="correo" v-model="correo" placeholder="Introduce tu correo">
        <span class="error">{{ errorcorreo }}</span>

        <label for="contrasena">Contraseña</label>
        <input type="password" id="contrasena" v-model="contrasena" placeholder="Introduce tu contraseña">
        <span class="error">{{ errorcontrasena }}</span>

        <label for="telefono">Teléfono</label>
        <input type="number" id="telefono" v-model="telefono" placeholder="Introduce tu teléfono">
        <span class="error">{{ errortelefono }}</span>
      </form>

      <button @click="guardar" class="btn-guardar">Guardar</button>
    </div>

    <div class="table-container">
      <table v-if="datos.length" class="styled-table">
        <thead>
          <tr>
            <th>Nombre</th>
            <th>Apellidos</th>
            <th>Edad</th>
            <th>Género</th>
            <th>Correo</th>
            <th>Contraseña</th>
            <th>Teléfono</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="dato in datos" :key="dato.nombre">
            <td>{{ dato.nombre }}</td>
            <td>{{ dato.apellidos }}</td>
            <td>{{ dato.edad }}</td>
            <td>{{ dato.genero }}</td>
            <td>{{ dato.correo }}</td>
            <td>{{ dato.contrasena }}</td>
            <td>{{ dato.telefono }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
.main-container {
  display: flex;
  justify-content: space-between;
  padding: 20px;
}

.form-container {
  background-color: #fffcf2;
  padding: 2rem;
  border-radius: 15px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
  width: 45%;
  border: 2px solid #ff6f61;
}

.table-container {
  width: 45%;
}

label {
  display: block;
  font-size: 1.1rem;
  color: #333;
  margin-bottom: 0.5rem;
}

input {
  width: 100%;
  padding: 0.5rem;
  margin-bottom: 1rem;
  border: 2px solid #ff6f61;
  border-radius: 5px;
  font-size: 1rem;
}

.error {
  color: #ff6f61;
  font-size: 0.9rem;
  margin-bottom: 1rem;
}

.btn-guardar {
  background-color: #ff6f61;
  color: white;
  padding: 0.8rem 1.5rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.btn-guardar:hover {
  background-color: #e55a4f;
}

.styled-table {
  width: 100%;
  border-collapse: collapse;
  margin: 1rem 0;
  font-size: 1rem;
  text-align: left;
}

.styled-table th,
.styled-table td {
  padding: 12px 15px;
  border: 1px solid #ddd;
}

.styled-table th {
  background-color: #ff6f61;
  color: white;
}

.styled-table tr {
  background-color: #f3f3f3;
}

.styled-table tr:nth-of-type(even) {
  background-color: #ffffff;
}
</style>
