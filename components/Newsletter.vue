<template>
  <section class='container my-5'>
    <div class='row mb-5'>
      <div class='col-lg-8 mx-auto'>
        <header class='mb-4'>
          <h2 class='text-center'>Contactanos</h2>
        </header>
        <form class="row" @submit.prevent="handleSubmit">
          <div class="form-group col-lg-6">
            <label for="firstname">Nombre</label>
            <input type="text" class="form-control" id="firstname" name="firstname" v-model="inputs.firstName">
          </div>
          <div class="form-group col-lg-6">
            <label for="lastname">Apellido</label>
            <input type="text" class="form-control" id="lastname" name="lastname" v-model="inputs.lastName">
          </div>
          <div class="form-group col-lg-6">
            <label for="input_email">Email</label>
            <input type="email" class="form-control" id="input_email" name="email" v-model="inputs.email">
          </div>
          <div class="form-group col-lg-6">
            <label for="phone">Telefono</label>
            <input type="text" class="form-control" id="phone" v-model="inputs.phoneNumber">
          </div>
          <div class="col-lg-3 ml-auto d-flex flex-column">
            <button :disabled="disableSubmit" type="submit" class="btn btn-primary submit">Enviar</button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>

<script>

const API_URL = 'https://5eed24da4cbc340016330f0d.mockapi.io/api/newsletter'

export default {
  name: 'Newsletter',
  data: () => ({
    inputs: {
      email: "",
      firstName: "",
      lastName: "",
      phoneNumber: ""
    },
    state: {
      loading: false,
    }
  }),
  methods: {
    handleSubmit: async function() {
      this.state.loading = true;
      const ctx = this;
      await fetch(API_URL, {
        method: "POST",
        body: JSON.stringify(this.inputs),
        headers: {"Content-type": "application/json; charset=UTF-8"}
      })
      .then(response => response.json()) 
      .then(json => console.log(json))
      .catch(err => console.log(err))
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
  header {
    position: relative;
  }
  header h2 {
    position: relative;
    z-index: 2;
   }
  header::before {
    content: "";
    position: absolute;
    z-index: 1;
    top: 50%;
    left: 0;
    width: 100%;
    height: 100%;
    background: url(/brush.webp);
    background-repeat: no-repeat;
    background-position: center bottom;
    background-size: contain;
    opacity: 0.3;
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
