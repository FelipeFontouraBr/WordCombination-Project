<template>
  <div>
    <div  id="slogan" class="text-center">
      <h1>NameGator</h1>
      <br/>
      <h6 class="text-secondary">Gerador de nomes utilizando Vue.js, GraphQL e Node</h6>
    </div>
    <div id="main"><!--Aqui é aonde vamos criar nossa aplicação-->
      <div class="container">
        <div class="row">
          <div class="col-md">
            <h5>Prefixos <span class="badge badge-info">0</span></h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group"><!--Aqui vamos criar listas-->
                  <li class="list-group-item">
                    A
                  </li>
                  <li class="list-group-item">
                    A
                  </li>
                   <li class="list-group-item">
                    A
                  </li>                  
                </ul>
                <br/> 
                <input class="form-control" type="text" placeholder="Digite o prefixo"/>
              </div>
            </div>
          </div>
          <div class="col-md">
            <h5>Sufixos <span class="badge badge-info">0</span></h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group"><!--Aqui vamos criar listas-->
                  <li class="list-group-item">
                    A
                  </li>
                  <li class="list-group-item">
                    A
                  </li>
                   <li class="list-group-item">
                    A
                  </li>                  
                </ul> 
                 <br/> 
                <input class="form-control" type="text" placeholder="Digite o sufixo"/>
              </div>
            </div>
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
      prefixes: ['Air', 'Jet', 'Flight'],
      sufixes: ['Hub', 'Station', 'Mart']
    }
  }
  
}
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
