<template>
  <header>
    <a href="#" @click="click=true" v-if="!click">myRandomNamer</a>
    <div v-if="click">
      <span @click="!click" :title="'Cierra el ' + name">x</span>

      <a
        v-for="(apartado, index) in menu"
        :href="apartado.ruta"
        :key="index"
        @click="!click"
      >{{apartado.titulo}}</a>
    </div>
  </header>
</template>

<script>
export default {
  name: "menu",
  data() {
    return {
      click: false,
      menu: [
        {
          titulo: "name",
          ruta: "/randomName"
        },
        {
          titulo: "color",
          ruta: "/randomColor"
        },
        {
          titulo: "font",
          ruta: "/randomFont"
        }
      ]
    };
  }
};
</script>

<style lang="scss" scoped>
$color: #99bdd1;

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
  color: rgb(58, 57, 57);
  height: auto;
  margin-top: 10vh;
  position: relative;

  div {
    position: relative;

    span {
      color: red;
      border: 1px solid red;
      padding: 1vh;
      position: absolute;
      right: 10vw;
    }
  }

  a {
    border: 10px solid darken($color, 20%);
    padding: 1vw;
    border-radius: 10px 0 10px;
    background: $color;
    text-decoration: none;
    font-size: 1.5em;
    color: white;
  }

  > a:hover,
  > div a:hover {
    box-shadow: 13px 0 13px grey;
    transform: translateY(-7px);
  }
}
</style>