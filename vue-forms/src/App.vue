<template>
  <div id="app">

    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Formulários no Vue</h1>
        <p class="lead">Treinando a manipulação de formulários</p>
      </div>
    </div>
    <div class="container">
      <div class="row">
        <!-- formulario -->
        <div class="col-sm-6">
          <h3>Preencha abaixo</h3>
          <form 
            @submit.prevent="enviar"
            @reset="resetar">

            <div class="form-group">
              <label>Nome:</label>
              <input type="text" class="form-control" placeholder="Seu nome" v-model.trim.lazy="desenvolvedor.nome">
            </div>
            <div class="form-group">
              <label>Endereço de email:</label>
              <input type="email" class="form-control" placeholder="Seu email" v-model.lazy="desenvolvedor.email">
            </div>
            <div class="form-group">
              <label>Idade:</label>
              <input type="number" class="form-control" placeholder="Sua idade" v-model.number="desenvolvedor.idade">
            </div>
            <div class="form-group">
              <p>Gênero:</p>
              <div class="form-check form-check-inline">
                <input type="radio" class="form-check-input" id="msd" value="Masculino"
                v-model="desenvolvedor.genero">
                <label class="form-check-label" for="msd">Masculino</label>
              </div>
              <div class="form-check form-check-inline">
                <input type="radio" class="form-check-input" id="fml" value="Feminino"
                v-model="desenvolvedor.genero">
                <label class="form-check-label" for="fml">Feminino</label>
              </div>
            </div>
            <div class="form-group">
              <label>Ocupação:</label>
              <select class="form-control" v-model="desenvolvedor.ocupacao">
                <option value="" disabled> Selecione uma opção ....... </option>
                <option 
                  v-for="(item, i) in ocupacoes" 
                  :key="i" 
                  :value="item"
                  :selected="item === 'Dev Full Stack'">
                  
                  {{ item }}
                
                </option>
              </select>
            </div>
            <div class="form-group">
              <p>Tecnologias:</p>
              <div class="form-check form-check-inline">
                <input type="checkbox" id="c1" class="form-check-input" value="JavaScript" v-model="desenvolvedor.tecnologias">
                <label class="form-check-label" for="c1">JavaScript</label>
              </div>
              <div class="form-check form-check-inline" >
                <input type="checkbox" id="c2" class="form-check-input" value="Vue JS" v-model="desenvolvedor.tecnologias">
                <label class="form-check-label" for="c2">Vue JS</label>
              </div>
              <div class="form-check form-check-inline">
                <input type="checkbox" id="c3" class="form-check-input" value="Vuex" v-model="desenvolvedor.tecnologias">
                <label class="form-check-label" for="c3">Vuex</label>
              </div>
              <div class="form-check form-check-inline">
                <input type="checkbox" id="c4" class="form-check-input" value="Vue Router" v-model="desenvolvedor.tecnologias">
                <label class="form-check-label" for="c4">Vue Router</label>
              </div>
            </div>
            <div class="form-group">
              <label for="txt-arear">Resumo de perfil:</label>
              <textarea id="txt-arear" class="form-control" placeholder="Conte-nos um pouco sobre você..." v-model="desenvolvedor.biografia"></textarea>
            </div>
            <div class="form-group">
              <AppRange
                inputClasses="form-control-range"
                label="Salario: "
                v-model.number="desenvolvedor.salario"
                min="1000"
                max="15000"
                step="500" />
            </div>
            <div class="form-group">
              <div class="form-check form-check-inline">
                <input type="checkbox" class="form-check-input" id="rec" v-model="desenvolvedor.notificacoes"
                true-value="Sim"
                false-value="Não">
                <label class="form-check-label" for="rec">Receber notificações por email</label>
              </div>
            </div>

            <button class="btn btn-secondary" type="reset">Resetar</button>
            <!-- <button class="btn btn-success" type="button" @click="enviar">Enviar</button> -->
            <button class="btn btn-success" type="submit">Enviar</button>
          </form>
        </div>
        <!-- saida -->
        <div class="col-sm-6">
          <h3>Saída</h3>
          <div class="card">
            <div class="card-header">Dados</div>
            <ul class="list-group list-group-flush">
              <li class="list-group-item"><strong>Nome:</strong> {{ desenvolvedor.nome }} </li>
              <li class="list-group-item"><strong>Email:</strong> {{ desenvolvedor.email }} </li>
              <li class="list-group-item"><strong>Idade:</strong> {{ desenvolvedor.idade }} </li>
              <li class="list-group-item"><strong>Gênero:</strong> {{ desenvolvedor.genero }} </li>
              <li class="list-group-item">
                <strong>Ocupação:</strong>
                {{ desenvolvedor.ocupacao }}
              </li>
              <li class="list-group-item">
                <strong>Tecnologias:</strong>
                <ul>
                  <li v-for="(item, i) in desenvolvedor.tecnologias" :key="i">
                    {{ item }}
                  </li>
                </ul>
              </li>
              <!-- <li class="list-group-item"><strong>Biografia:</strong>{{ desenvolvedor.biografia }} </li> -->
              <li class="list-group-item">
                <strong>Biografia:
                </strong>
                <!-- <pre>{{ desenvolvedor.biografia }} </pre> -->
                <div style="white-space: pre">{{ desenvolvedor.biografia }} </div>
              </li>

              <!-- <li class="list-group-item"><strong>Receber notificações?</strong> {{ desenvolvedor.notificacoes ? 'Sim' : 'Não' }} </li> -->
              <li class="list-group-item"><strong>Receber notificações?</strong> {{ desenvolvedor.notificacoes }} </li>
              <li class="list-group-item"><strong>Salário Pretendido </strong> {{ desenvolvedor.salario }} </li>
            </ul>
            <div class="card-header">Model</div>
            <div class="card-body">
              <!-- <pre><code>{{ {'nome': 'Plínio Naves'} }}</code></pre> -->
              <!-- DEBUGGER VUE  igual ao (form | json) no angular-->
              <pre><code>{{ desenvolvedor }}</code></pre>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>

import AppRange from './components/Range';

export default {
  components: {
    AppRange
  },
  data () {
    return {
      desenvolvedor: {},
      valoresPadroes: {
        nome: '',
        email: '',
        idade: 28,
        biografia: 'Sou Dev Fron-End',
        genero: 'Masculino',
        tecnologias: [],
        notificacoes: 'Não',
        ocupacao: '',
        salario: 1000
      },
      ocupacoes: [
        'Dev Fron-End (Web)',
        'Dev Fron-End (Mobile)',
        'Dev Fron-End (Web e Mobile)',
        'Dev Back-End',
        'Dev Full Stack',
      ]
    }
  },
  methods: {
    enviar() {
      const form = Object.assign({}, this.desenvolvedor);
      console.log(' FORM SEND ', this.desenvolvedor)
    },
    resetar() {
      this.desenvolvedor = Object.assign({}, this.valoresPadroes);
    }
  },
  created() {
    this.resetar();
  }
}
</script>




<style scoped>
  .btn {
    margin-right: 5px;
  }
</style>