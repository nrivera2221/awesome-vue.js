<template>
  <div class="container">
    <form id="form" action="">

      <div>
        <label> Color de fondo</label>
        <input type="text" v-model="bgColor" placeholder="darkgreen">
      </div>
      <div>
        <label> Color de texto </label>
        <input type="text" v-model="txtColor" placeholder="darkgreen">
      </div>
      <div>
        <label> Mostrar texto <input type="checkbox" v-model="isShow" /></label>
      </div>
      <div>
        <label>Bordes </label>
        <input v-model="borde" type="range" min="0" max="200">
      </div>
      <div>
        <label>Contenido Textual</label>
        <input type="text" v-model="texto">
      </div>
      <div>
        <label> Tipografía</label>
        <select v-model="typografiaSelecionada">
          <option v-for="(typografia, index) in typografias " :key="index" :value="typografia">
            {{ typografia }}
          </option>
        </select>
      </div>
      <div>
        <label> Opaco <input type="checkbox" v-model="isBlur" /> </label>

      </div>
      <div class="btn">

        <label>Tamaño de letra </label>
        <label><input type="radio" id="one" value="pequeno" v-model="picked" /> Pequeño</label>
        <label> <input type="radio" id="two"  value="mediano" v-model="picked" /> Mediano</label>
        <label> <input type="radio" id="three"  value="grande" v-model="picked" /> Grande</label>

      </div>
    </form>

    <!-- cuadrado -->
    <div id="square" :style="{ backgroundColor: bgColor, borderRadius: borde + 'px' }"
      :class="{ 'blur-effect': isBlur }">
      <h1 v-show="isShow" :style="{ color: txtColor, fontFamily: typografiaSelecionada, fontSize: fontSize }">
        {{ texto }}
      </h1>
    </div>
  </div>



</template>

<script setup>
import { computed, ref } from 'vue';
const bgColor = ref('pink')
const txtColor = ref('white')
const isShow = ref(true)
const borde = ref(0)
const texto = ref('Awesome Vue.js')
const typografias = ["serif ", "cursive", "sans-serif", "fantasy", "Monospace"]

const typografiaSelecionada = ref(typografias[1])
const isBlur = ref('')
const picked = ref('mediano')

const fontSize = computed(() => {
  if (picked.value === 'pequeno') {
    return '16px';
  } else if (picked.value === 'mediano') {
    return '32px';
  } else if (picked.value === 'grande') {
    return '48px';
  }
  return '32px';
});
</script>

<style scoped>
#square {
  width: 400px;
  height: 400px;
  border: 4px solid #3607f2;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  border-color: #007bff; /* Color del borde al enfocarse */
        outline: none; /* Elimina el contorno predeterminado */
        box-shadow: 0 0 5px rgba(0, 123, 255, 0.5); /* Efecto de foco */
  background-color: bisque;
  margin: 120px;
  padding: 15px;
}

#form>div {
  display: flex;
  flex-direction: column;
  width: 300px;
  padding-right: 20px;
}

.blur-effect {
  filter: blur(5px);
}
</style>