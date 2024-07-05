<script setup>
import { ref } from 'vue'

const user = ref({
  name: '',
  surname: '',
  email: 'pilgerrafael772@gmail.com',
  city: '',
  state: '',
  zip: '',
  avatar: '',
  hobbies: [],
  preferredLanguage: '',
  biografia: '',
  confirmacao: '',
  senha:''
})

function confirmacao() {
     if ( confirmacao.value != user.senha){
      return alert('A senha esta incorreta: ')
     } else{
      senhavalida.value = true
     }
}

const states = [
  { uf: 'AC', name: 'Acre' },
  { uf: 'AL', name: 'Alagoas' },
  { uf: 'AP', name: 'Amapá' },
  { uf: 'AM', name: 'Amazonas' },
  { uf: 'BA', name: 'Bahia' },
  { uf: 'CE', name: 'Ceará' },
  { uf: 'DF', name: 'Distrito Federal' },
  { uf: 'ES', name: 'Espírito Santo' },
  { uf: 'GO', name: 'Goiás' },
  { uf: 'MA', name: 'Maranhão' },
  { uf: 'MT', name: 'Mato Grosso' },
  { uf: 'MS', name: 'Mato Grosso do Sul' },
  { uf: 'MG', name: 'Minas Gerais' },
  { uf: 'PA', name: 'Pará' },
  { uf: 'PB', name: 'Paraíba' },
  { uf: 'PR', name: 'Paraná' },
  { uf: 'PE', name: 'Pernambuco' },
  { uf: 'PI', name: 'Piauí' },
  { uf: 'RJ', name: 'Rio de Janeiro' },
  { uf: 'RN', name: 'Rio Grande do Norte' },
  { uf: 'RS', name: 'Rio Grande do Sul' },
  { uf: 'RO', name: 'Rondônia' },
  { uf: 'RR', name: 'Roraima' },
  { uf: 'SC', name: 'Santa Catarina' },
  { uf: 'SP', name: 'São Paulo' },
  { uf: 'SE', name: 'Sergipe' },
  { uf: 'TO', name: 'Tocantins' }
]

const mostrarPerfil = ref(false)

function handleFileUpload(e) {
  const target = e.target
  console.log(target)
  if (target && target.files) {
    const file = target.files[0]
    user.value.avatar = URL.createObjectURL(file)
  }
}

function salvarPerfil() {
  mostrarPerfil.value = true
}
</script>

<template>
  <div class="container">
    <main>
      <h1>Editor de Perfil</h1>
      <transition name="form" mode="out-in">
        <section v-if="mostrarPerfil">
          <div class="mt-5 mb-3">
            <p v-for="(value, key) of user" :key="key">{{ key }}: {{ value }}</p>
            <img v-if="user.avatar" class="avatar" :src="user.avatar" />
          </div>
          <button class="btn btn-info" @click="mostrarPerfil = false">Esconder</button>
        </section>
        <form v-else class="row g-3 was-validated" @submit.prevent="salvarPerfil()" validate>
          <div class="col-md-4">
            <label for="nameField" class="form-label">Nome</label>
            <input type="text" class="form-control" id="nameField" v-model="user.name" required />
            <div class="invalid-feedback">Nome obrigatório</div>
          </div>

          <div class="col-md-4">
            <label for="surnameField" class="form-label">Sobrenome</label>
            <input
              type="text"
              class="form-control"
              id="surnameField"
              v-model="user.surname"
              required
            />
            <div class="invalid-feedback">Sobrenome obrigatório</div>
          </div>


          <div class="col-md-4">
            <label for="emailField" class="form-label">E-mail</label>
            <div class="input-group">
              <span class="input-group-text" id="emailFieldPrepend">@</span>
              <input
                type="email"
                class="form-control"
                id="emailField"
                aria-describedby="emailFieldPrepend"
                v-model="user.email"
                required
              />
              <div class="invalid-feedback">E-mail obrigatório.</div>
              <div class="valid-feedback">E-mail válido!</div>
            </div>

          </div>
          <div class="col-md-4">
            <label for="nameField" class="form-label">senha:</label>
            <input type="text" class="form-control" id="nameField" placeholder="senha:" v-model="user.senha" required />
            <div class="invalid-feedback">senha obrigatoria</div>

          </div>

          <div class="col-md-4">
            <label for="nameField" class="form-label">confirmaçao de senha:</label>
            <input type="text" class="form-control" id="nameField" @blur="confirmacao()" v-model="user.confirmacao" required />
          </div>


          <div>
            <div class="col-md-6">
              <label for="cityField" class="form-label">Cidade</label>
              <input type="text" class="form-control" id="cityField" v-model="user.city" />
            </div>
            <div class="col-md-4">
              <label for="stateField" class="form-label">Estado</label>
              <select class="form-select" id="stateField" v-model="user.state">
                <option selected disabled value="">Selecionar...</option>
                <option v-for="state of states" :key="state.uf" :value="state.uf">
                  {{ state.name }}
                </option>
              </select>
            </div>
          </div>
          <div class="col-md-5">
            <label for="zipField" class="form-label">CEP</label>
            <input type="text" class="form-control" id="zipField" v-model="user.zip" />
          </div>

          <div class="col-md-6">
            <label for="avatarField" class="form-label">Avatar</label>
            <input type="file" class="form-control" id="avatarField" @change="handleFileUpload($event)"/>
          </div>

          <div class="col-8">
            <p class="mb-0">Hobbies</p>
            <input class="ms-3 me-1" type="checkbox" id="hobbiesField" value="esportes" v-model="user.hobbies"/>
            <label for="hobbiesField">Esportes</label>
            <input class="ms-3 me-1" type="checkbox" id="hobbiesField" value="música" v-model="user.hobbies"/>
            <label for="hobbiesField">Música</label>
            <input class="ms-3 me-1" type="checkbox" id="hobbiesField" value="viagens" v-model="user.hobbies"/>
            <label for="hobbiesField">Viagens</label>
            <input class="ms-3 me-1" type="checkbox" id="hobbiesField" value="leitura" v-model="user.hobbies"/>
            <label for="hobbiesField">Leitura</label>
          </div>

          <div class="col-6">
            <p class="mb-0">Linguagem preferida</p>
            <input class="ms-3 me-1" type="radio" id="langC" value="C" v-model="user.preferredLanguage"/>
            <label for="langC">C</label>
            <input class="ms-3 me-1" type="radio" v-model="user.preferredLanguage" value="Java" id="langJava"/>
            <label for="langJava">Java</label>
            <input class="ms-3 me-1" type="radio" v-model="user.preferredLanguage" value="Python" id="langPython"/>
            <label for="langPython">Python</label>
            <input class="ms-3 me-1" type="radio" v-model="user.preferredLanguage" value="Javascript" id="langJs"/>
            <label for="langJs">JavaScript</label>
          </div>

          <div  class="col-md-10">
            <label for="bioField" class="form-label">Biografia</label>
            <textarea id="bioField" v-model="user.biografia" required></textarea>
          </div>

          <div class="col-12">
            <button class="btn btn-primary" type="submit">Enviar</button>
          </div>
        </form>
      </transition>
    </main>
  </div>
</template>

<style scoped>


.container {
  width: 90%;
  max-width: 600px;
  margin: 40px auto 0;
  padding: 20px;
  border: 15px solid #000146;
  border-radius: 15px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  background-color: #571892; 
  color: black;
}

.main {
  padding: 20px;
}

.avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  object-fit: cover;
}

.text-center {
  text-align: center;
}

.form-group {
  margin-bottom: 1.5rem; 
}

label {
  margin-bottom: 1rem;
}
</style>