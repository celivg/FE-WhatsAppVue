<script>
export default {
  name: 'ChatBox',
  props: {
    mensajes: {
      type: Array,
      required: true
    }
  }
}
</script>

<template>
  <div class="chatbox">
    <div
      v-for="(mensaje, idx) in mensajes"
      :key="idx"
      :class="mensaje.side === 'left' ? 'text-start' : 'text-end'"
    >
      <span
        ><b>{{ mensaje.name }}</b></span
      >
      <br />
      <p
        class="msj p-2 rounded"
        :style="{
          backgroundColor: mensaje.color
        }"
      >
        {{ mensaje.mensaje }}
      </p>
    </div>
  </div>
</template>

<style scoped>
.chatbox {
  background-color: #f2eeea;
  padding: 1rem;
  border-radius: 10px;
  height: 80vh;
  overflow-y: scroll;
}

.msj {
  display: inline-block;
  word-wrap: break-word;
  max-width: 80%;
  box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
}
</style>
