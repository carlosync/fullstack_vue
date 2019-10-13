<template>
  <div>
    <div id="slogan" class="text-center">
      <h1>Domains Generator</h1>
      <br/>
      <h6>Generate of Domains - Vuejs e Node.</h6>
    </div>

    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <h5>Prefixes <span class="badge badge-info">{{ prefixes.length }}</span></h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="prefix in prefixes" v-bind:key="prefix">
                    <div class="row">
                      <div class="col-md">
                          {{ prefix }}
                      </div>
                      <div class="col-md text-right">
                          <button class="btn btn-info" title="Remover" v-on:click="deletePrefix(prefix)">
                            <span class="fa fa-trash"></span>
                          </button>
                      </div>
                    </div>
                  </li>
                </ul>
                <br/>
                <div class="input-group">
                  <input type="text" class="form-control" v-model="prefix" v-on:keyup.enter="addPrefix(prefix)" 
                    placeholder="Digite o prefix"/>
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addPrefix(prefix)">
                      <span class="fa fa-plus"></span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-md">
            <h5>Sufixes <span class="badge badge-info">{{ sufixes.length }}</span></h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="sufix in sufixes" v-bind:key="sufix">
                    <div class="row">
                      <div class="col-md">
                        {{ sufix }}
                      </div>
                      <div class="col-md text-right">
                          <button class="btn btn-info" title="Remover" v-on:click="deleteSufix(sufix)">
                            <span class="fa fa-trash"></span></button>
                      </div>
                    </div>     
                  </li>
                </ul>
                <br/>
                <div class="input-group">
                  <input type="text" class="form-control" v-model="sufix" v-on:keyup.enter="addSufix(sufix)" 
                    placeholder="Digite o sufix"/>
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addSufix(sufix)">
                      <span class="fa fa-plus"></span>
                    </button>
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
                      <a class="btn btn-info" v-bind:href="domain.checkout" target="_blank">
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
import 'bootstrap/dist/css/bootstrap.css';
import 'font-awesome/css/font-awesome.css';

export default {
  name: 'app',
  data: function () {
    return {
      prefix: "",
      sufix: "",
      prefixes: ['Air', 'Jet', 'Flight'],
      sufixes:  ['Hub', 'Station', 'Mart']
    };
  },

  methods: {
    addPrefix(prefix){
      this.prefixes.push(prefix);
      this.prefix = "";
    },

    deletePrefix(prefix){
      this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
    },

    addSufix(sufix){
      this.sufixes.push(sufix);
      this.sufix = "";
    },

    deleteSufix(sufix){
      this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
    }
  },
  computed: {
    domains(){
      const domains = [];
      for(const prefix of this.prefixes){
        for (const sufix of this.sufixes){
          const name = prefix + sufix;
          const url = name.toLowerCase();
          const checkout = `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com.br`;
          domains.push({
            name,
            checkout
          });
        }
      }
      return domains;
    }
  }
}
</script>

<style>

html, body{
  font-size: 14px;
}

#slogan{
  background-color:#17a2b8; /*  #0082C7; #17a2b8*/
  height: 100px;
  padding-top: 10px;
  padding-bottom: 8px;
  /* margin-bottom: 40px; */
  color: #f1f1f1;
}

#main{
  background-color: #f1f1f1;
  padding-top: 30px;
  padding-bottom: 30px;
}
</style>