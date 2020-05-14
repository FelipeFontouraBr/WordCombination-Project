<template>
  <div>
    <div  id="slogan" class="text-center">
      <h1>NameAir</h1>
      <br/>
      <h6 class="text-secondary">Gerador de nomes utilizando Vue.js, GraphQL e Node</h6>
    </div>
    <div id="main"><!--Aqui é aonde vamos criar nossa aplicação-->
      <div class="container">
        <div class="row">
          <div class="col-md">
            <h5>Prefixos <span class="badge badge-info">{{ prefixes.length }}</span></h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group"><!--Aqui vamos criar listas-->
                  <li class="list-group-item" v-for="prefix in prefixes" v-bind:key="prefix">
                    <div class="row">
                      <div class="col-md">
                        {{ prefix }}
                      </div>
                      <div class="col-md text-right">
                        <button class="btn btn-info" v-on:click="deletePrefix(prefix)"><span class="fa fa-trash"></span></button><!--Botão de delete / o (prefix) esta vindo do v-for-->
                      </div>
                    </div>
                  </li>
                </ul>
                <br/>
                <div class="input-group"><!--Formulário de entrada de dados--> 
                  <input class="form-control" type="text" v-model="prefix" v-on:keyup.enter="addPrefix(prefix)" placeholder="Digite o prefixo"/><!--V-model irá fazer a interação da caixa de texto com a propriedade prefix(variavel)/keyup.enter, toda vez que der enter vai adicionar-->
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addPrefix(prefix)"><span class="fa fa-plus"></span></button>
                  </div>
                </div>                
              </div>
            </div>
          </div>
          <div class="col-md">
            <h5>Sufixos <span class="badge badge-info">{{ sufixes.length }}</span></h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group"><!--Aqui vamos criar listas-->
                  <li class="list-group-item" v-for="sufix in sufixes" v-bind:key="sufix">
                    <div class="row">
                      <div class="col-md">
                        {{ sufix }}
                      </div>
                      <div class="col-md text-right">
                        <button class="btn btn-info" v-on:click="deleteSufix(sufix)"><span class="fa fa-trash"></span></button><!--Botão de delete-->
                      </div>
                    </div>                    
                  </li>
                </ul> 
                 <br/>
                <div class="input-group"><!--Formulário de entrada de dados--> 
                  <input class="form-control" type="text" v-model="sufix" v-on:keyup.enter="addSufix(sufix)" placeholder="Digite o sufixo"/>
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addSufix(sufix)"><span class="fa fa-plus"></span></button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <br/>
        <h5>Domains <span class="badge badge-info">{{ domains.length }}</span></h5>
        <div class="card">
          <div class="card-body">
            <ul class="list-group">
              <li class="list-group-item" v-for="domain in domains" v-bind:key="domain.name">
                <div class="row">
                  <div class="col-md">
                    {{ domain.name }}
                  </div>
                  <div class="col-md text-right">
                    <a class="btn btn-info" href="https://github.com/FelipeFontouraBr" target="_blank">
                      <span class="fa fa-shopping-cart"></span>
                    </a>
                  </div>
                </div>                
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css"
import "font-awesome/css/font-awesome.css"

export default {
  name: 'App',
  data() {//Método 
    return { //retorno um objeto que será disponivel para o sistema de tamplate
      prefix: "",
      sufix: "",
      prefixes: ['Air', 'Jet', 'Flight'],
      sufixes: ['Hub', 'Station', 'Mart']
    }
  },
  //Nesse objeto vamos definir as funções para funcionarem
  methods: {
    addPrefix(prefix) {//variavel local chamada (prefix), que vamos adicionar
      this.prefixes.push(prefix);//Aqui vamos colocar os prefixos que serão colocados
      this.prefix = "";//Depois que clicar, limpa o campo de adicionar
      },
    deletePrefix(prefix) {
      this.prefixes.splice(this.prefixes.indexOf(prefix), 1);//splice->No primeiro parametro irá receber o elemento que vamos deletar
      },
    deleteSufix(sufix) {
      this.sufixes.splice(this.sufixes.indexOf(sufix), 1);//1 pq quero eliminir 1 elemento do array
      },    
    addSufix(sufix) {
      this.sufixes.push(sufix);
      this.sufix = "";
      }
  },
//Computed Propries -> Recurso do Vue que faz a aplicação ficar mais perfomática e isso baseado em sistema de reatividade do Vue
    computed: { //Funções que vão estar envolvidas com um watcher e tudo o que elas utilizarem, o Vue irá gerenciar e só ira invocar se for necessario
      domains(){ //Toda vez que prefix ou sufixe for alterado, irá invocar essa função
        console.log("generating domains...")
        const domains = [];//vai gerar um array vazio para que eu posso gerar os prefixo s sufixos
        for (const prefix of this.prefixes) {//Colocar this. para ver as propriedades existentes deste componente
          for (const sufix of this.sufixes) {
            const name = prefix + sufix;
            const url = name.toLowerCase();
            const checkout = `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com`;//Link
              domains.push({//Objeto:
                name,
                checkout
              });
          }
        }
        return domains;
      }
    },
  /*created() {//essa propriedade é bom para buscar dados no meu backend, API para trazer info para aplicação
    this.generate(); //quando carrega a pagina, gera as informações
  }*/
};
</script>

<style>
#slogan {
  margin-top: 30px;
  margin-bottom: 30px;
}
#main {
  background-color: #F1F1F1;
  padding-top: 30px;
  padding-bottom: 30px;  
}
</style>
