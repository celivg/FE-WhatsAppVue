<script>
export default {
  name: 'UserPov',
  data() {
    return {
      mensaje: '',
      color: '#dcf8c6'
    }
  },
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  methods: {
    enviarMensaje() {
      this.$emit('enviar-mensaje', this.mensaje, this.color, this.user.name.first, this.user.side)

      this.mensaje = ''
    }
  },
  emits: ['enviar-mensaje']
}
</script>

<template>
  <div class="container">
    <div class="card">
      <img :src="user.picture.large" class="card-img-top" :alt="user.name.first" />
      <div class="card-body">
        <h5 class="card-title">{{ user.name.first }} {{ user.name.last }}</h5>

        <form class="d-flex flex-column gap-2" @submit.prevent="enviarMensaje">
          <input v-model="color" class="w-100" type="color" />
          <textarea v-model="mensaje"></textarea>
          <button class="btn btn-custom">Enviar</button>
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>
.btn-custom {
  background-color: #128c7e;
  color: white;
}
</style>
