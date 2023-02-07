<template>
  <section class='container my-5'>
    <div class='row mb-5'>
      <div class='col-lg-8 mx-auto'>
        <HeadingBrush
          marginBottom='4'
          content='Contactanos'
          headingType="h2"
        />
        <form class="row" @submit.prevent="handleSubmit">
          <div class="form-group col-lg-6">
            <label for="firstname">Nombre</label>
            <input
              type="text"
              class="form-control"
              id="firstname"
              name="firstname"
              v-model="inputs.firstName"
              required
            >
          </div>
          <div class="form-group col-lg-6">
            <label for="lastname">Apellido</label>
            <input
              type="text"
              class="form-control"
              id="lastname"
              name="lastname"
              v-model="inputs.lastName"
              required
            >
          </div>
          <div class="form-group col-lg-6">
            <label for="input_email">Email</label>
            <input
              type="email"
              class="form-control"
              id="input_email"
              name="email"
              v-model="inputs.email"
              required
            >
          </div>
          <div class="form-group col-lg-6">
            <label for="phone">Telefono</label>
            <input
              type="text"
              class="form-control"
              id="phone"
              v-model="inputs.phoneNumber"
              required
            >
          </div>
          <div class="col-lg-3 ml-auto d-flex flex-column">
            <button :disabled="disableSubmit" type="submit" class="btn btn-primary submit">Enviar</button>
          </div>
        </form>
      </div>
      <div class='col-lg-8 mx-auto mt-3'>
        <div v-if='state.success' class="alert alert-success" role='alert'>
          {{state.success}}
        </div>
        <div v-if='state.error' class="alert alert-danger" role='alert'>
          {{state.error}}
        </div>
      </div>
    </div>
  </section>
</template>

<script>

const API_URL = 'https://5eed24da4cbc340016330f0d.mockapi.io/api/newsletter'

const defaultState = {
  loading: false,
  error: '',
  success: ''
}
const defaultInputs = {
  email: '',
  firstName: '',
  lastName: '',
  phoneNumber: ''
}

export default {
  name: 'Newsletter',
  data: () => ({
    inputs: defaultInputs,
    state: defaultState
  }),
  methods: {
    resetState: function() {
      this.state = defaultState
    },
    resetInputs: function() {
      this.inputs = defaultInputs
    },
    handleSubmit: async function() {
      this.resetState()

      this.state.loading = true

      const ctx = this

      await fetch(API_URL, {
        method: "POST",
        body: JSON.stringify(this.inputs),
        headers: {"Content-type": "application/json; charset=UTF-8"}
      })
      .then(async response => {
        if (!response.ok) {
          throw await response.json()
          return
        }
        ctx.state.success = 'Formulario enviado correctamente'
      })
      .catch(err => {
        console.log(err)
        ctx.state.error = 'No se pudo enviar el formulario'
      })
      .finally(() => ctx.state.loading = false)
    }
  },
  computed: {
    disableSubmit() {
      return (
        this.state.loading ||
        !(this.inputs.email && this.inputs.firstName && this.inputs.lastName && this.inputs.phoneNumber)
      )
    }
  }
}
</script>

<style scoped>
  input:focus {
    box-shadow: 0 0 0 0.05rem #D8AD3D;
    border-color: #D8AD3D;
  }
  button.submit {
    background-color: #D8AD3D;
    border-color: #D8AD3D;
    border-radius: 30px;
    font-weight: bold;
  }
  button.submit:hover {
    background-color: #009CD9;
    border-color: #009CD9;
  }
  button.submit:focus {
    box-shadow: none;
  }
  button[disabled] {
    background: #CFCFCF;
    border-color: #CFCFCF;
    color: #FFFFFF;
    opacity: 0.5;
  }
  button[disabled]:hover {
    background: #CFCFCF;
    border-color: #CFCFCF;
    color: #FFFFFF;
    opacity: 0.5;
  }
</style>
