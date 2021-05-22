<template>
  <div id="app" :class="saudacao.class">
    <div class="relogio">
      <div :class="saudacao.fundo">
        <div id="bomdia">
          {{ saudacao.texto }}
        </div>
        <div id="local">Local</div>
        <div id="hora">
          {{ hora }}
        </div>
        <div id="dias">
          {{ semana }}
          {{ dia }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment'
moment.locale('pt-br')

export default {
  name: 'App',
  data: () => ({
    semana: moment().format('dddd'),
    dia: moment().format('DD/MM'),
    hora: moment().format('HH:mm'),
    h: moment().add(4, 'hours').format('H')
  }),
  computed: {
    saudacao() {
      const valor = Number(this.h)
      switch (true) {
        case valor >= 0 && valor <= 5:
          return {
            texto: 'Boa Madrugada',
            class: 'madrugada'
          }
        case valor < 12:
          return {
            texto: 'Bom Dia',
            class: 'dia'
          }
        case valor < 17:
          return {
            texto: 'Boa Tarde',
            class: 'tarde',
            fundo: 'back'
          }
        case valor < 19:
          return {
            texto: 'Boa Tarde',
            class: 'tardezinha',
            fundo: 'back'
          }
        default:
          return {
            texto: 'Boa Noite',
            class: 'noite'
          }
      }
    }
  }
}
</script>

<style lang="scss">
@font-face {
  font-family: malvie;
  src: url(./assets/Fonte/Malvie.otf);
}
body {
  margin: 0;
  padding: 0;
  color: white;
}
#app {
  height: 100vh;
  background-position: center;
  background-size: cover;
}
.relogio {
  width: 400px;
  height: 400px;
  margin: auto;
  padding-top: 100px;
}
#bomdia {
  margin-top: 60px;
  text-align: center;
  padding: 50px;
  font-family: malvie;
  font-weight: bold;
  font-size: 55px;
}
#local {
  text-align: center;
}
#hora {
  text-align: center;
  font-size: 60px;
  font-family: malvie;
  font-weight: bold;
}
#dias {
  height: 70px;
  line-height: 10px;
  text-align: center;
  font-size: 25px;
  
}
.madrugada {
  background-image: url(./assets/5.jpg);
}
.dia {
  background-image: url(./assets/1.jpg);
  color: rgb(0, 8, 5);
}
.tarde {
  background-image: url(./assets/2.jpg);
}
.tardezinha {
  background-image: url(./assets/3.jpg);
}
.noite {
  background-image: url(./assets/4.jpg);
}
.back{
  border-radius: 10px;
  background: rgba(7, 7, 7, 0.473);
}
</style>
