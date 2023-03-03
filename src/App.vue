<script>

let id = 0;

export default {
  data() {
    return {
      message1: 'LISTING',
      message2: 'Actividades',
      message3: 'About',
      message4: 'Extra',

      text: '',
      type: null,
      tareas: []
    }
    
  },
  methods: {
    onInput(texto) {
      this.text = texto.target.value;
    },
    agregarTarea() {
      if(this.text !== '' && this.type !== null)
      {
        this.tareas.push({id: id++, valor: this.text, tipo: this.type, lista: false});
        this.text = '';
        this.type = null;
      }
    },
    eliminarTarea(obj) {
      this.tareas = this.tareas.filter(temp => temp !== obj);
    },
    limpiar() {
      this.tareas = this.tareas.filter(temp => temp.lista !== true);
    }
  }
}
</script>

<template>
  <header>
    <a href="" class="logo">
      <img src="./assets/check.png" alt="Logo">
      <h2 class="nombre" >{{ message1 }}</h2>
    </a>
    <nav>
      <a target="_blank" href="https://fabianmarianojimenezherrera.000webhostapp.com/tareabootstrap/" class="nav-link">{{ message2 }}</a>
      <a target="_blank" href="https://fabianmarianojimenezherrera.000webhostapp.com/trabajo01/" class="nav-link">{{ message3 }}</a>
      <a href="" class="nav-link">{{ message4 }}</a>
    </nav>
  </header>

  <!-- Parte inicial de la página web,
      aquí se muestra un slider -->
  
  <section class="galery">
    <div class="phrase">
      <h3>Organiza tus labores, planea las tareas de tu empresa, gestiona tus actividades.</h3>
    </div>
    <div class="images">
      <img class="img1" src="./assets/listado1.jpg">
      <img class="img2" src="./assets/listado2.jpg">
      <img class="img3" src="./assets/listado3.jpg">
    </div>
  </section>

  <!-- Parte principal de la página web,
      aquí se escriben las tareas -->

  <section class="input-area">
    <form @submit.prevent="agregarTarea()">
      <!-- Aquí se ingresa la tarea-->
      <h4>Escribe tus actividades a realizar</h4>
      <input v-model="text" placeholder="ej. Crear una página web">
      <p class="texto">{{text}}</p>
      
      
      <!-- Aquí se ingresa el tipo-->
      <h4>Selecciona el tipo de actividad</h4>
      <div class="options">
        <label>
          <input type="radio" name="tipo" value="personal" v-model="type">
          <span class="bubble personal"></span>
          <div>Personal</div>
        </label>
        <label>
          <input type="radio" name="tipo" value="trabajo" v-model="type">
          <span class="bubble trabajo"></span>
          <div>Trabajo</div>
        </label>
        <label>
          <input type="radio" name="tipo" value="otro" v-model="type">
          <span class="bubble otro"></span>
          <div>Otro</div>
        </label>
      </div>
      <!-- Enviamos los datos-->
      <div class="actions">
        <input type="submit" value="Agregar Tarea">
        <button @click="limpiar()">Limpiar Tareas Hechas</button>
      </div>

    </form>
  </section>

  <!-- Parte intermedia de la página web,
      aquí se despliegan las tareas -->
  <div class="list-area">
    <p v-for="tarea in tareas" :key="tarea.id" :class="`item ${tarea.lista && 'lista'}`">
      <label>
        <input type="checkbox" v-model="tarea.lista">
        <span :class="`bubble ${tarea.tipo}`"></span>
      </label>
      <div class="content">
        <input type="text" v-model="tarea.valor">
      </div>      
      
      <div class="actions">
        <button class="delete" @click="eliminarTarea(tarea)">Eliminar</button>
      </div>
      
    </p>
  </div>
</template>
