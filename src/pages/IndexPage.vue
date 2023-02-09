<template>
  <q-page class="container" padding>
    <p class="text-h4">Fomulário</p>

      <q-form
      class="row q-col-gutter-md"
      @submit="onSubmit"
      @reset="onReset"
      ref = "myForm"
      >
        <q-input
          class="col-md-12 col-sm-12 col-xs-12"
          clearable
          outlined
          v-model="form.nome"
          color="deep-purple"
          label="Nome e sobrenome"
          :rules="[
            val => val && val.length > 0 || 'Nome e sobrenome obrigatorios'
          ]"
        >
        <template v-slot:prepend>
          <q-icon name = "person"/>
        </template>
      </q-input>

      <q-input
          class="col-md-12 col-sm-12 col-xs-12"
          outlined
          v-model.number="form.idade"
          type="number"
          label="Ideade"
          :rules="[
            val => val !== null && val !== '' || 'Idade obrigatoria',
            val => val > 0 && val < 100 || 'Coloque uma idade real'
          ]"
        >
          <template v-slot:prepend>
            <q-icon name = "person"/>
          </template>
        </q-input>

        <q-input
          class="col-md-12 col-sm-12 col-xs-12"
          outlined
          v-model="form.email"
          label="Email"
          suffix=@gmail.com
          :loading="false"
          :rules="[
            val => val && val.length > 0 || 'email obrigatorio',
          ]"
        >
        <template v-slot:prepend>
          <q-icon name="mails"/>
        </template>
        </q-input>

        <q-input
            class="col-md-12 col-sm-12 col-xs-12"
            outlined
            v-model="form.telefone"
            label="Telefone"
            mask="(##) ##### - ####"
            unmasked-value
            :rules= "[
              val => val && val.length > 0 || 'Telefone obrigatorio',
              val => val.length === 11 || 'Coloque um telefone válido'
            ]"
          />
          <q-select
          class="col-md-12 col-sm-12 col-xs-12"
           outlined
           v-model="form.tipoPessoa"
           :options="optionsTipoPessoa"
           label="Tipo de pessoa"
           emit-value
           map-options
           :rules = "[
              val => val && val.length > 0 || 'Tipo de pessoa obrigatório'
           ]"
           />
           <span class="text-bold">Sexo</span>
           <q-option-group
             class="col-md-12 col-sm-12 col-xs-12"
             :options="optionsSexo"
             label="Sexo"
             type="radio"
             v-model="form.sexo"
           />
           <span class="text-bold">Possui alguma dificultade?</span>
           <q-option-group
           class="col-md-12 col-sm-12 col-xs-12"
            :options="optionsDificultade"
            label="Dificultades"
            type="checkbox"
            color="red"
            v-model="form.dificultade"
           />
           <q-toggle
            v-model="form.notificacoes"
            color="primary"
            icon="mail"
            label="Recibir notificaciones?"
            size="lg"
            />
          <div class="col-12">
            <q-btn
            label="Cadastrar"
            type="submit"
            color="primary"
            class="float-right"
            />
            <q-btn
            class="float-right text-grey-10 q-mr-md"
            label="Reset"
            type="reset"
            color="default"
            />
          </div>
      </q-form>
  </q-page>
</template>

<script>
/* import { defineComponent } from 'vue' */

export default {
  name: 'IndexPage',
  data () {
    return {
      form: {
        nome: '',
        idade: null,
        email: '',
        telefone: '',
        tipoPessoa: '',
        sexo: 'O',
        dificultade: [],
        notificacoes: false
      },
      optionsTipoPessoa: [
        { label: 'Pessoa Física', value: 'pf' },
        { label: 'Pessoa Jurídica', value: 'pj' }
      ],
      optionsSexo: [
        { label: 'Homen', value: 'H' },
        { label: 'Mulher', value: 'M' },
        { label: 'Outros', value: 'O' }
      ],
      optionsDificultade: [
        { label: 'Motoras', value: 'Mot', color: 'negative' },
        { label: 'Visuais', value: 'Vis', color: 'positive' },
        { label: 'Auditivas', value: 'Aud', color: 'purple' }
      ]
    }
  },
  methods: {
    onSubmit () {
      this.$q.notify({
        message: 'Cadastro realizado con sucesso!',
        color: 'positive',
        icon: 'task_alt'
      })
      this.onReset()
    },
    async onReset () {
      await this.resetForm()
      this.$refs.myForm.resetValidation()
    },
    resetForm () {
      this.form = {
        nome: '',
        idade: null,
        email: '',
        telefone: '',
        tipoPessoa: '',
        sexo: 'O',
        dificultade: [],
        notificacoes: false
      }
    }
  }
}
</script>
