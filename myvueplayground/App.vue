<template>
  <header>
    <a href="#" @click="click=true" v-if="!click">Click para ver el Menú</a>
    <div v-if="click">
      <a
        v-bind:href="apartado.ruta"
        v-for="(apartado, index) in menu"
        :key="index"
        @click="click=false"
      >{{apartado.titulo}}</a>

      <span @click="click=false">x</span>
    </div>
  </header>
</template>

<script>
export default {
  name: "navigation",
  data() {
    return {
      click: false,
      menu: [
        {
          titulo: "Doctor Arruga",
          ruta: "/doctorArruga"
        },
        {
          titulo: "Puto$elmo",
          ruta: "/doctorArruga"
        },
        {
          titulo: "StereooTipo",
          ruta: "/stereootipo"
        },
        {
          titulo: "Señor Eme",
          ruta: "/mistereme"
        }
      ]
    };
  }
};
</script>

<style lang="scss" scoped>
$color: #536976;

* {
  font-family: Arial, Helvetica, sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

header {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  flex-flow: wrap;
  color: white;
  height: auto;
  margin-top: 10vh;
}

a {
  border: 10px solid darken($color, 20%);
  padding: 1vw;
  border-radius: 10px 0 10px;
  background: $color;
  text-decoration: none;
  font-size: 1.5em;
  color: white;

  &:hover {
    box-shadow: 13px 0 13px grey;
    transform: translateY(-7px);
  }
}
</style>