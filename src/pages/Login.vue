<template>
    <div class="q-pa-md">
        <q-form
            @submit="onSubmit"
            @reset="onReset"
            class="q-gutter-md"
        >
            <q-input
                filled
                v-model="email"
                label="Seu e-mail"
                lazy-rules
                :rules="[ val => val && val.length > 0 || 'Por favor, digite alguma coisa']"
            />
            <q-input
                filled
                v-model="senha"
                label='Sua senha'
                type='password'
                lazy-rules
                :rules="[ val => val && val.length > 0 || 'Por favor, digite alguma coisa']"
            />
            <div>
                <q-btn label="Entrar" type="submit" color="primary"/>
                <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm"/>
            </div>
        </q-form>
        <q-btn label="Não possui uma conta?" to="/register" outline rounded color="primary"/>
    </div>
</template>

<script>
import firebase from 'firebase'
export default {
  data () {
    return {
      email: null,
      senha: null
    }
  },
  methods: {
    onSubmit () {
      firebase.auth().signInWithEmailAndPassword(this.email, this.senha).then(
        (user) => {
          this.$router.push('home')
          console.log('me mama')
        },
        (err) => {
          alert('Aconteceu algo de errado. ' + err.message)
        }
      )
    },
    onReset () {
      console.log('Resetou.')
      this.email = null
      this.senha = null
      this.apelido = null
    }
  },
  mounted () {
    if (firebase.auth().currentUser) {
      this.$router.push('home')
    }
  }
}
</script>
