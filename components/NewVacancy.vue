<template>
  <div class="body">
    <div class="container mt-6">
      <br />
      <div class="text-light text-center">
        <h1><strong>New vacancy</strong></h1>
        <p>Fill out the form and publish your vacancy</p>
        <br />
      </div>
      <div action="" class="form-control">
        <h4 class="text-center">General Information</h4>
        <br />

        <form class="item" v-on:submit.prevent="newVacancy">
          <div class="form-group">
            <label for="jobTitleVacancy">Tittle</label>
            <input
              type="tittle"
              class="form-control"
              id=""
              aria-describedby="jobTitleHelp"
              placeholder="Ex: React Developer"
              v-model="titulo"
            />
          </div>

          <div>
            <label for="companyName">Company</label>
            <input
              type="company"
              class="form-control"
              id=""
              aria-describedby="companyHelp"
              placeholder="Company"
              v-model="empresa"
            />
          </div>
          <div>
            <label for="companyLocation">Location</label>
            <input
              type="location"
              class="form-control"
              id=""
              aria-describedby="locationHelp"
              placeholder="Ex: Mexico or Remote"
              v-model="ubicacion"
            />
          </div>
          <div>
            <label for="salaryUSD">Salary(USD)</label>
            <input
              type="salary"
              class="form-control"
              id=""
              aria-describedby="salaryHelp"
              placeholder="Ex: $500 USD"
              v-model="salario"
            />
          </div>
          <div>
            <label for="employmentContract">Contract</label>
            <select name="select" class="form-control" v-model="contrato">
              <option value="Undefined">Undefined</option>
              <option value="Fixed" selected>Fixed</option>
              <option value="Services">Services</option>
            </select>
          </div>
          <div>
            <label for="jobDescritption">Job Description</label>
            <div class="form-group purple-border">
              <input class="form-control" v-model="descripcion" />
            </div>
          </div>
          <label for="skills">Required Skills</label>
          <div class="form-group purple-border m-1">
            <input class="form-control" v-model="skills" />
          </div>
          <br />
          <div class="submit d-flex justify-content-around">
            <button type="submit" class="get-started-btn p-1 m-1 enviar">
              Create
            </button>
          </div>
          <br />
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>
.c-1 {
  color: white !important;
}
.mt-6 {
  position: relative;
  top: 10% !important;
}
.body {
  font-family: 'Mukta', sans-serif;
  width: 100vw;
  height: 100vh;
  background-color: #100e17;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
}
.wrapper {
  display: grid;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}

div.boton {
  justify-content: space-evenly;
  padding: 5px 0;
}

button {
  width: 100px;
  height: 38px;
  margin-top: 3px;
}

.enviar {
  color: #fff;
  background: #006837;
  box-shadow: none;
}
</style>

<script>
export default {
  data() {
    return {
      titulo: '',
      empresa: '',
      ubicacion: '',
      salario: '',
      contrato: '',
      salario: '',
      descripcion: '',
      skills: '',
    }
  },
  methods: {
    async newVacancy() {
      let data = {
        titulo: this.titulo,
        empresa: this.empresa,
        ubicacion: this.ubicacion,
        salario: this.salario,
        contrato: this.contrato,
        descripcion: this.descripcion,
        skills: this.skills,
      }
      console.log(data)
      try {
        await this.$axios.post('api/vancancy/create', data).then((response) => {
          this.$swal({
            icon: 'success',
            title: 'Nueva Vacante Creada',
          })
        })
      } catch (error) {
        this.$swal({
          icon: 'error',
          title: error,
        })
      }
    },
  },
}
</script>
