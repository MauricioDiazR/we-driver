<template>
  <div class="divlogin">    
    <div class="container">
      <div class="contenido">
        <figure id="logotipo">
          <img class="img" :src="LoginLogo" width="200">
        </figure>
        <h2>{{title}}</h2>
        <form @submit.prevent="sendForm">
          <input
            type="email"
            :class="{ error: validaEmail }"
            placeholder="Email"
            v-model="form.email"
          />
          <input
            type="password"
            v-if="form.type != 1"
            :class="{ error: validaPassword }"
            placeholder="password"
            v-model="form.password"
          />
          <button>{{title}}</button>
          <button v-if="form.type == 0">Sign in with Google</button>
        </form>

        <a
          href="javascript:void(0)"
          @click="form.type = 1"
          v-if="form.type == 0"
        >Forgot your password?</a>
        <router-link to="../registro" style="font-size: 18px; color: black;" v-if="form.type == 0">Sign up</router-link>
        <a
          href="javascript:void(0)"
          @click="form.type = 0"
          v-if="form.type == 1"
          style="font-size: 18px; color: black;"
        >Cancel</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    props: {
        LoginLogo: {
        type: String,
        default: require("@/assets/img/logo.jpg")
        },
        FondoTrasparente: {
        type: String,
        default: require("@/assets/img/fondo_transparente.jpg")
        }
    },

  data: function() {
    return {
      form: {
        type: 0, //0 = login, 1 = recuperar contraseña
        email: "",
        password: ""
      },
      objetoEstilo: {
        color: 'red'
      }

    };
  },
  methods: {
    sendForm() {
      if (this.validaType()) {
        console.log(this.form);
      }
    },
    validaType() {
      if (this.form.type == 0 && !this.validaEmail && !this.validaPassword) {
        return true;
      } else if (this.form.type == 1 && !this.validaEmail) {
        return true;
      } else {
        return false;
      }
    }
  },
  computed: {
    validaEmail() {
      var exp = /^(([^<>()[\]\.,;:\s@\"]+(\.[^<>()[\]\.,;:\s@\"]+)*)|(\".+\"))@(([^<>()[\]\.,;:\s@\"]+\.)+[^<>()[\]\.,;:\s@\"]{2,})$/i;
      if (exp.test(this.form.email)) {
        return false;
      } else {
        return true;
      }
    },
    validaPassword() {
      var exp = /^(?=.*\d)(?=.*[a-záéíóúüñ]).*[A-ZÁÉÍÓÚÜÑ]/;
      if (exp.test(this.form.password)) {
        return false;
      } else {
        return true;
      }
    },
    title() {
      return this.form.type == 0
        ? "Sign in"
        : "Reset password";
    }
  }
};
</script>

<style scoped>

html,body {
  padding: 0px;
  margin: 0px;
  width: 100%;
  height: 100vh;
  font-family: "RobotoMono-Bold";
  color: #333333;
}

.divlogin {
  background: url('../../assets/img/fondo_transparente.jpg');
  background-color: rgba(0, 0, 0, 0.5);
  background-size: cover;
  background-position: center center;
  width: 100%;
  height: 100vh;
  display: flex;
  align-content: center;
  align-items: center;
}

.divlogin .container {
  text-align: center;
  margin: auto;
}

.divlogin .container .contenido {
  width: 100%;
  max-width: 300px;
  background: rgba(255, 255, 255, 1);
  padding: 20px;
  display: inline-block;
  font-family: "RobotoMono-Bold";
  margin-left: auto;
}

.divlogin .container .contenido h2 {
  margin-top: 0px;
  margin-bottom: 20px;
  color: red;
  font-size: 2em;
  font-family: "RobotoMono-Bold";
}

.divlogin .container .contenido input {
  height: 30px;
  margin: 0px;
  margin-bottom: 20px;
  border: 2px solid #acacac;
  padding: 10px;
  width: 70%;
  font-family: "RobotoMono-Bold";
}

.divlogin .container .contenido input.error {
  border-bottom: 3px solid red;
}

.divlogin .container .contenido button {
  height: 50px;
  margin: 10px;
  padding: 10px;
  border: 0px;
  width: 80%;
  background: red;
  color: #ffffff;
  font-size: 18px;
  border-radius: 5px;
  font-family: "RobotoMono-Bold";
}

.divlogin .container .contenido a {
  margin: 10px;
  font-size: 12px;
  color: #333333;
  font-family: "RobotoMono-Bold";
  text-decoration: none;
  display: block;
}

#logotipo {
  margin: 0px;
}
</style>
