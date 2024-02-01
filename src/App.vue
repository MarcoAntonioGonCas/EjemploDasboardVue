<script setup>
import { RouterLink, RouterView } from 'vue-router'
import { ref ,onMounted } from 'vue';
import HelloWorld from './components/HelloWorld.vue'
import Chart from 'chart.js/auto'




const canvas = ref();

onMounted(()=>{




  const datos = {
      "error": null,
      "data": [
          {
              "idUbicacion": 3,
              "nombreUbicacion": "Entrada general",
              "dia": "2024-01-08T00:00:00",
              "numeroAccesos": 7
          },
          {
              "idUbicacion": 3,
              "nombreUbicacion": "Entrada general",
              "dia": "2024-01-22T00:00:00",
              "numeroAccesos": 3
          },
          {
              "idUbicacion": 3,
              "nombreUbicacion": "Entrada general",
              "dia": "2024-01-30T00:00:00",
              "numeroAccesos": 24
          },
          {
              "idUbicacion": 3,
              "nombreUbicacion": "Entrada general",
              "dia": "2024-01-28T00:00:00",
              "numeroAccesos": 73
          },
          {
              "idUbicacion": 3,
              "nombreUbicacion": "Entrada general",
              "dia": "2024-01-29T00:00:00",
              "numeroAccesos": 7
          },
          {
              "idUbicacion": 3,
              "nombreUbicacion": "Entrada general",
              "dia": "2024-01-31T00:00:00",
              "numeroAccesos": 8
          },
          {
              "idUbicacion": 1,
              "nombreUbicacion": "Salon b",
              "dia": "2024-01-05T00:00:00",
              "numeroAccesos": 34
          },
          {
              "idUbicacion": 1,
              "nombreUbicacion": "Salon b",
              "dia": "2024-01-07T00:00:00",
              "numeroAccesos": 3
          },
          {
              "idUbicacion": 1,
              "nombreUbicacion": "Salon b",
              "dia": "2024-01-08T00:00:00",
              "numeroAccesos": 93
          },
          {
              "idUbicacion": 1,
              "nombreUbicacion": "Salon b",
              "dia": "2024-01-26T00:00:00",
              "numeroAccesos": 1
          },
          {
              "idUbicacion": 1,
              "nombreUbicacion": "Salon b",
              "dia": "2024-01-28T00:00:00",
              "numeroAccesos": 16
          },
          {
              "idUbicacion": 1,
              "nombreUbicacion": "Salon b",
              "dia": "2024-01-09T00:00:00",
              "numeroAccesos": 6
          },
          {
              "idUbicacion": 1,
              "nombreUbicacion": "Salon b",
              "dia": "2024-01-10T00:00:00",
              "numeroAccesos": 1
          },
          {
              "idUbicacion": 1,
              "nombreUbicacion": "Salon b",
              "dia": "2024-01-22T00:00:00",
              "numeroAccesos": 1
          },
          {
              "idUbicacion": 1,
              "nombreUbicacion": "Salon b",
              "dia": "2024-01-30T00:00:00",
              "numeroAccesos": 2
          },
          {
              "idUbicacion": 2,
              "nombreUbicacion": "Salon CC",
              "dia": "2024-01-07T00:00:00",
              "numeroAccesos": 1
          },
          {
              "idUbicacion": 2,
              "nombreUbicacion": "Salon CC",
              "dia": "2024-01-08T00:00:00",
              "numeroAccesos": 36
          },
          {
              "idUbicacion": 2,
              "nombreUbicacion": "Salon CC",
              "dia": "2024-01-28T00:00:00",
              "numeroAccesos": 3
          },
          {
              "idUbicacion": 2,
              "nombreUbicacion": "Salon CC",
              "dia": "2024-01-22T00:00:00",
              "numeroAccesos": 2
          },
          {
              "idUbicacion": 2,
              "nombreUbicacion": "Salon CC",
              "dia": "2024-01-26T00:00:00",
              "numeroAccesos": 5
          },
          {
              "idUbicacion": 2,
              "nombreUbicacion": "Salon CC",
              "dia": "2024-01-30T00:00:00",
              "numeroAccesos": 9
          }
      ]
  }


  const labels = [];

  const datasets = {};

  datos.data.forEach(acceso => {


    const {nombreUbicacion,dia,numeroAccesos} = acceso;
    const fechaDia = new Date(dia);

    // agregamos los labels
    if(labels.indexOf(fechaDia) == -1){

      labels.push(fechaDia);

    }

    // Cremos los dasets
    if( !datasets[nombreUbicacion] ){

      datasets[nombreUbicacion] = {
        label:nombreUbicacion,
        data:[]
      }
    }

    // Agregamos los ultimos
    datasets[nombreUbicacion].data.push({
      x:new Date(fechaDia),
      y:numeroAccesos
    });
    


});



new Chart(canvas.value,{
    type:"bar",
    data:{
      labels,
      datasets:Object.values(datasets)
    },
    
    
})




});





</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>

    <canvas id="canvas" ref="canvas" ></canvas>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
