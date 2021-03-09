<template>
  <q-page class="container" padding>
    <div class="row justify-center">
      <p class="text-h4">Cadastro</p>
    </div>
    <div class="row justify-center">
      <q-form
        @submit="onSubmit"
        @reset="onReset"
        class="q-col-gutter-md"
        ref="myForm"
      >
        <q-input
          outlined
          v-model="form.nome"
          label="Nome"
          color="deep-purple"
          class="col-md-12 col-sm-12 col-xs-12"
          :rules="[ val => val && val.length > 0 || 'Por favor, preencha o nome!']"
        >
          <template v-slot:prepend>
            <q-icon name="person"/>
          </template>
        </q-input>

        <q-input
          v-model.number="form.idade"
          color="purple"
          type="number"
          outlined
          label="Idade"
          class="col-md-12 col-sm-12 col-xs-12"
          :rules="[
            val => val !== null && val !== '' || 'Por favor, preencha a idade!',
            val => val > 0 && val < 100 || 'Digite uma idade válida'
          ]"
        >
          <template v-slot:prepend>
            <q-icon name="event"/>
          </template>
        </q-input>

        <q-input
          v-model="form.email"
          color="purple"
          suffix="@gmail.com"
          outlined
          label="E-mail"
          class="col-md-12 col-sm-12 col-xs-12"
          :rules="[ val => val && val.length > 0 || 'Por favor, preencha o e-mail!']"
        >
          <template v-slot:prepend>
            <q-icon name="email"/>
          </template>
        </q-input>

        <q-input
          v-model="form.telefone"
          color="purple"
          outlined
          label="Telefone"
          mask="(##) #####-####"
          unmasked-value
          class="col-md-12 col-sm-12 col-xs-12"
          :rules="[
            val => val && val.length > 0 || 'Por favor, preencha o campo de telefone!',
            val => val.length === 11 || 'Digite um número válido'
          ]"
        >
          <template v-slot:prepend>
            <q-icon name="phone"/>
          </template>
        </q-input>

        <q-select
          outlined
          color="purple"
          v-model="form.tipoPessoa"
          :options="optionsTipoPessoa"
          label="Tipo de pessoas"
          class="col-md-12 col-sm-12 col-xs-12"
          :rules="[ val => val && val.length > 0 || 'Selecione tipo de pessoa!']"
          emit-value
          map-options
        />

        <div class="col-12">
          <q-btn
            label="Cadastrar"
            type="submit"
            color="purple"
            class="float-right"
          />
          <q-btn
            label="Resetar"
            type="reset"
            color="default"
            class="float-right text-grey-10 q-mr-md"
          />
        </div>
      </q-form>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      form: {
        nome: '',
        idade: null,
        email: '',
        telefone: '',
        tipoPessoa: ''
      },
      optionsTipoPessoa: [
        { label: 'Pessoa física', value: 'pf' },
        { label: 'Pessoa jurídica', value: 'pj' }
      ]
    }
  },
  methods: {
    onSubmit () {
      this.$q.notify({
        message: 'Cadastro realizado com sucesso!',
        color: 'positive',
        icon: 'check_circle'
      })
      this.onReset()
    },
    async onReset () {
      await this.resetForm()
      this.$refs.myForm.resetValidation()
    },
    async resetForm () {
      this.form = {
        nome: '',
        idade: null,
        email: '',
        telefone: '',
        tipoPessoa: ''
      }
    }
  }
}
</script>
