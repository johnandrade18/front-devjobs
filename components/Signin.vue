<template>
  <div class="body d-flex justify-content-center">
    <div id="signinContainer" class="Container">
      <div class="card card-container">
        <form class="form-signin" v-on:submit.prevent="login">
          <span id="reauth-email" class="reauth-email"></span>
          <input
            type="email"
            id="inputEmail"
            class="form-control"
            placeholder="Dirección de correo"
            required
            autofocus
            v-model="email"
          />
          <input
            type="password"
            id="inputPassword"
            class="form-control"
            placeholder="Contraseña"
            required
            v-model="password"
          />
          <button
            class="btn btn-lg btn-primary btn-block btn-signin"
            type="submit"
          >
            Iniciar sesión
          </button>
        </form>
        <!-- /form -->
      </div>
      <!-- /card-container -->
    </div>
    <!-- /container -->
  </div>
</template>
<script>
export default {
  name: 'signin',
  data() {
    return {
      email: '',
      password: '',
    }
  },
  methods: {
    async login() {
      let data = {
        email: this.email,
        password: this.password,
      }
      try {
        let response = await this.$auth.loginWith('local', { data: data })
        if (response.status == 200 && response.data.code == 100) {
          localStorage.token = response.data.token
          localStorage.rol = response.data.rol
          localStorage.username = response.data.username
          console.log(response.data.rol)
          this.$router.push('jobslist')
        }
      } catch (error) {
        this.$swal({
          icon: 'error',
          title: error.message,
        })
      }
    },
  },
}
</script>

<style scoped>
#signinContainer {
  display: flex;
  justify-content: center;
  align-items: center;
}
.body {
  font-family: 'Mukta', sans-serif;
  -ms-overflow-style: hidden !important;
  overflow-y: hidden !important;
  width: 100vw;
  height: 100vh;
  background-color: #100e17;
  background-repeat: no-repeat;
  background-size: cover;
}
html {
  height: 100%;
  background-repeat: no-repeat;
  background-image: linear-gradient(rgb(104, 145, 162), rgb(12, 97, 33));
}

.card-container.card {
  max-width: 350px;
  padding: 40px 40px;
}

.btn {
  font-weight: 700;
  height: 36px;
  -moz-user-select: none;
  -webkit-user-select: none;
  user-select: none;
  cursor: default;
}

/*
 * Card component
 */
.card {
  background-color: #f7f7f7;
  /* just in case there no content*/
  padding: 20px 25px 30px;
  margin: 0 auto 25px;
  margin-top: 50px;
  /* shadows and rounded borders */
  -moz-border-radius: 2px;
  -webkit-border-radius: 2px;
  border-radius: 2px;
  -moz-box-shadow: 0px 2px 2px rgba(0, 0, 0, 0.3);
  -webkit-box-shadow: 0px 2px 2px rgba(0, 0, 0, 0.3);
  box-shadow: 0px 2px 2px rgba(0, 0, 0, 0.3);
}

.profile-img-card {
  width: 96px;
  height: 96px;
  margin: 0 auto 10px;
  display: block;
  -moz-border-radius: 50%;
  -webkit-border-radius: 50%;
  border-radius: 50%;
}

/*
 * Form styles
 */
.profile-name-card {
  font-size: 16px;
  font-weight: bold;
  text-align: center;
  margin: 10px 0 0;
  min-height: 1em;
}

.reauth-email {
  display: block;
  color: #404040;
  line-height: 2;
  margin-bottom: 10px;
  font-size: 14px;
  text-align: center;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

.form-signin #inputEmail,
.form-signin #inputPassword {
  direction: ltr;
  height: 44px;
  font-size: 16px;
}

.form-signin input[type='email'],
.form-signin input[type='password'],
.form-signin input[type='text'],
.form-signin button {
  width: 100%;
  display: block;
  margin-bottom: 10px;
  z-index: 1;
  position: relative;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

.form-signin .form-control:focus {
  border-color: rgb(104, 145, 162);
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgb(104, 145, 162);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgb(104, 145, 162);
}

.btn.btn-signin {
  /*background-color: #4d90fe; */
  background-color: rgb(104, 145, 162);
  /* background-color: linear-gradient(rgb(104, 145, 162), rgb(12, 97, 33));*/
  padding: 0px;
  font-weight: 700;
  font-size: 14px;
  height: 36px;
  -moz-border-radius: 3px;
  -webkit-border-radius: 3px;
  border-radius: 3px;
  border: none;
  -o-transition: all 0.218s;
  -moz-transition: all 0.218s;
  -webkit-transition: all 0.218s;
  transition: all 0.218s;
}

.btn.btn-signin:hover,
.btn.btn-signin:active,
.btn.btn-signin:focus {
  background-color: rgb(12, 97, 33);
}

.forgot-password {
  color: rgb(104, 145, 162);
}

.forgot-password:hover,
.forgot-password:active,
.forgot-password:focus {
  color: rgb(12, 97, 33);
}
</style>
