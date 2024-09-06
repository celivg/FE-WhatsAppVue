<script>
import axios from 'axios'

import ChatBox from './ChatBox.vue'
import UserPov from './UserPov.vue'

export default {
  name: 'WhatsApp',
  components: {
    ChatBox,
    UserPov
  },
  data() {
    return {
      userLeft: {},
      userRight: {},
      mensajes: []
    }
  },
  async created() {
    try {
      const url = 'https://randomuser.me/api/?results=2'
      const { data } = await axios.get(url)

      this.userLeft = { ...data.results[0], side: 'left' }
      this.userRight = { ...data.results[1], side: 'right' }
    } catch (error) {
      console.error(error)
    }
  },
  methods: {
    enviarMensaje(mensaje, color, name, side) {
      this.mensajes.push({ mensaje, color, name, side })
    }
  }
}
</script>

<template>
  <div class="container mt-2">
    <div class="d-flex align-items-center">
      <img
        src="https://static.vecteezy.com/system/resources/previews/018/930/564/original/whatsapp-logo-whatsapp-icon-whatsapp-transparent-free-png.png"
        alt=""
        width="100"
      />
      <h1>WhatsAppChafa</h1>
    </div>
    <div class="row">
      <UserPov
        :user="userLeft"
        @enviar-mensaje="enviarMensaje"
        class="col-4"
        v-if="Object.keys(userLeft).length > 0"
      />
      <ChatBox class="col-4" :mensajes="mensajes" />
      <UserPov
        :user="userRight"
        @enviar-mensaje="enviarMensaje"
        class="col-4"
        v-if="Object.keys(userLeft).length > 0"
      />
    </div>
  </div>
</template>

<style scoped></style>
