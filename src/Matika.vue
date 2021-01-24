<template>
  <main>
    <header class="nadpis">
      <h1>Matematika</h1>
    </header>
    <div class="zadanie">
      <p>
        <span class="c1">{{ cislo[0] }}</span>
        <span class="z">{{ cislo[2] }}</span>
        <span class="c2">{{ cislo[1] }}</span>
      </p>
    </div>
    <div class="vysledok">
      <div @click="odpoved(moznosti[0])" class="v vysl">
        <p>{{ moznosti[0] }}</p>
      </div>
      <div @click="odpoved(moznosti[1])" class="v vysl">
        <p>{{ moznosti[1] }}</p>
      </div>
      <div @click="odpoved(moznosti[2])" class="v vysl">
        <p>{{ moznosti[2] }}</p>
      </div>
    </div>

    <div class="hura">
      <img src="/ok.svg" alt="ok" />
      <p>OK 😁</p>
    </div>
    <div class="zle">
      <img src="/not.svg" alt="nok" />
      <p>NIE 😏</p>
    </div>

    <input
      @input="zmena"
      type="range"
      id="mcislo"
      name="mcislo"
      list="tickmarks"
      min="10"
      max="100"
      value="20"
      step="10"
    />
    <datalist id="tickmarks">
      <option value="10" label="10"></option>
      <option value="20" label="20"></option>
      <option value="50" label="50"></option>
      <option value="100" label="100"></option>
    </datalist>

    <div class="nastavenia">
      {{ cisla[2] }}
      {{ cisla[3] }}
      {{ hranicaZadani }}
    </div>
  </main>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      hranicaZadani: 20,
      znamienko: 0,
      cisla: [],
      final: false,
      sprav: true,
      componentKey: 0,
      xxx: 0,
    }
  },
  computed: {
    cislo(xxx) {
      let x = parseInt(this.hranicaZadani)
      let c1 = x + 1
      let c2 = x + 1
      if (this.znamienko == 0) {
        while (c1 + c2 > x) {
          c1 = Math.floor(Math.random() * (x + 1) + (this.xxx - this.xxx))
          c2 = Math.floor(Math.random() * (x + 1))
        }
      }
      if (this.znamienko == 1) {
        while (c1 - c2 <= 0) {
          c1 = Math.floor(Math.random() * (x + 1))
          c2 = Math.floor(Math.random() * (x + 1))
        }
      }
      this.cisla = [c1, c2, ' + ', c1 + c2]
      return [c1, c2, ' + ', c1 + c2]
    },
    moznosti(xxx) {
      let pozicia = 1
      let x1 = 1
      let x2 = 1
      let x3 = 1
      pozicia = Math.floor(Math.random() * 3 + 1)
      if (pozicia === 1) {
        x1 = this.cisla[3]
        x2 = this.cisla[3] - 3
        x3 = this.cisla[3] + 5
        return [x1, x2, x3]
      }
      if (pozicia === 2) {
        x2 = this.cisla[3]
        x1 = this.cisla[3] - 3
        x3 = this.cisla[3] + 5
        return [x1, x2, x3]
      }
      if (pozicia === 3) {
        x3 = this.cisla[3]
        x1 = this.cisla[3] - 3
        x2 = this.cisla[3] + 5
        return [x1, x2, x3]
      }
    },
  },
  methods: {
    zmena(e) {
      this.hranicaZadani = e.target.value
    },
    odpoved(a) {
      document.querySelector('.zadanie').style.display = 'none'
      document.querySelector('.vysledok').style.display = 'none'
      if (a === this.cisla[3]) {
        this.sprav = true
        document.querySelector('.hura').style.display = 'block'
      } else {
        this.sprav = false
        document.querySelector('.zle').style.display = 'block'
      }
      this.final = true
      this.xxx += 1
      setTimeout(function () {
        this.final = false
        document.querySelector('.zadanie').style.display = 'block'
        document.querySelector('.vysledok').style.display = 'grid'
        document.querySelector('.hura').style.display = 'none'
        document.querySelector('.zle').style.display = 'none'
      }, 2000)
    },
  },
}
</script>

<style scoped>
.hura {
  margin: 100px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 5rem;
  color: black;
  display: none;
}
.zle {
  margin: 100px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 5rem;
  color: black;
  display: none;
}
.maxCislo {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 1rem;
  color: black;
}
</style>
