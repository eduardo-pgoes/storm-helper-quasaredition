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
                label="Sua senha"
                type="password"
                lazy-rules
                :rules="[ val => val && val.length > 0 || 'Por favor, digite alguma coisa']"
            />
            <q-input
                filled
                v-model="apelido"
                label="Seu apelido"
                lazy-rules
                :rules="[ val => val && val.length > 0 || 'Por favor, digite alguma coisa']"
            />
            <div>
                <q-btn label="Registrar" type="submit" color="primary"/>
                <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm"/>
            </div>
        </q-form>
    </div>
</template>

<script>
import firebase from 'firebase'
export default {
  data () {
    return {
      email: null,
      senha: null,
      apelido: null
    }
  },
  methods: {
    onSubmit () {
      firebase.auth().createUserWithEmailAndPassword(this.email, this.senha).then(
        (user) => {
          let email = this.email
          let apelido = this.apelido
          this.$router.replace('login')
          firebase.firestore().collection('users').add({ email: email, nome: apelido })
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
  }
}
</script>
