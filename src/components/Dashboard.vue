<template>
  <div id="burger-table">
    <Message :msg="msg" v-show="msg" />
    <section>
      <ul id="burger-table-heading">
        <li class="order-id">#:</li>
        <li>Cliente:</li>
        <li>Pão:</li>
        <li>Carne:</li>
        <li>Opcionais:</li>
        <li>Ações:</li>
      </ul>
    </section>

    <section id="burger-table-rows">
      <ul class="burger-table-row" v-for="burger in burgers" :key="burger.id">
        <li class="order-number">{{ burger.id }}</li>
        <li>{{ burger.nome }}</li>
        <li>{{ burger.pao }}</li>
        <li>{{ burger.carne }}</li>
        <ul class="optional-list">
          <li v-for="(opcional, index) in burger.opcionais" :key="index">
            {{ opcional }}
          </li>
        </ul>
        <li>
          <select
            name="status"
            class="status"
            @change="updateBurger($event, burger.id)"
          >
            <option value="">Selecione</option>
            <option
              v-for="s in status"
              :key="s.id"
              :value="s.tipo"
              :selected="burger.status == s.tipo"
            >
              {{ s.tipo }}
            </option>
          </select>
          <button class="delete-btn" @click="deleteBurger(burger.id)">
            Cancelar
          </button>
        </li>
      </ul>
    </section>
  </div>
</template>

<script>
import Message from './Message.vue'

export default {
  name: 'Dashboard',
  components: {
    Message
  },
  data() {
    return {
      burgers: null,
      burger_id: null,
      status: [],
      msg: null
    }
  },
  methods: {
    async getPedidos() {
      const req = await fetch('http://localhost:3000/burgers')

      const data = await req.json()

      this.burgers = data

      //Resgatar os status
      this.getStatus()
    },
    async getStatus() {
      const req = await fetch('http://localhost:3000/status')
      const data = await req.json()
      this.status = data
    },
    async deleteBurger(id) {
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: 'DELETE'
      })

      const res = await req.json()

      this.msg = 'Pedido removido com sucesso!'

      setTimeout(() => (this.msg = ''), 3000)

      this.getPedidos()
    },
    async updateBurger(event, id) {
      const option = event.target.value
      const dataJson = JSON.stringify({ status: option })
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: dataJson
      })

      const res = await req.json()

      this.msg = `O pedido N°${res.id} foi atualizado para: ${res.status}!`

      setTimeout(() => (this.msg = ''), 3000)
    }
  },
  mounted() {
    this.getPedidos()
  }
}
</script>

<style scoped>
* {
  list-style-type: none;
}
#burger-table {
  max-width: 1200px;
  margin: 0 auto;
}
#burger-table-heading,
#burger-table-rows,
.burger-table-row {
  display: flex;
  flex-wrap: wrap;
}
#burger-table-heading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #333;
}
#burger-table-heading li,
.burger-table-row li,
.burger-table-row ul {
  width: 19%;
}
.burger-table-row {
  width: 100%;
  padding: 12px;

  border-bottom: 1px solid #ccc;
}
#burger-table-heading .order-id,
.burger-table-row .order-number {
  width: 5%;
}
select {
  padding: 12px 6px;
  margin-right: 12px;
}
.optional-list,
.optional-list li {
  list-style-type: disc;
  width: 100px;
}
.delete-btn {
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
}
.delete-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
