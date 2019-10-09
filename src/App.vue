<template>
  <div>
    <div id="slogan" class="text-center">
      <h1>
        <span class="fa fa-check">Dinossaurus</span>
      </h1>
      <hr />
      <h6 class="text-secondary">Gerador de nomes utlizando Vue.js</h6>
    </div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <h5>
              Prefixos
              <span class="badge badge-info">{{ prefixes.length }}</span>
            </h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="prefix in prefixes" v-bind:key="prefix">
                    <div class="row">
                      <div class="col-md">{{ prefix }}</div>
                      <div class="col-md text-right">
                        <button class="btn btn-info" v-on:click="removePrefix(prefix)">
                          <span class="fa fa-trash"></span>
                        </button>
                      </div>
                    </div>
                  </li>
                </ul>
                <br />
                <div class="input-group">
                  <input
                    class="form-control"
                    type="text"
                    placeholder="Digite o prefixo"
                    v-model="prefix"
                    v-on:keyup.enter="addPrefix(prefix)"
                  />
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
            <h5>
              Sufixos
              <span class="badge badge-info">{{ sufixes.length }}</span>
            </h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="sufix in sufixes" v-bind:key="sufix">
                    <div class="row">
                      <div class="col=md">{{ sufix }}</div>
                      <div class="col-md text-right">
                        <button class="btn btn-info" v-on:click="removeSufix(sufix)">
                          <span class="fa fa-trash"></span>
                        </button>
                      </div>
                    </div>
                  </li>
                </ul>
                <br />
                <div class="input-group">
                  <input
                    class="form-control"
                    type="text"
                    placeholder="Digite o sufixo"
                    v-model="sufix"
                    v-on:keyup.enter="addSufix(sufix)"
                  />
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
        <br />
        <h5>
          Domínios
          <span class="badge badge-info">{{ generate().length }}</span>
        </h5>
        <div class="card">
          <div class="class-body">
            <ul class="list-group">
              <li class="list-group-item" v-for="domain in generate()" v-bind:key="domain">{{ domain }}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
export default {
	name: "app",
	data: function() {
		return {
			prefix: "",
			sufix: "",
			prefixes: ["Air", "Jet", "Flight"],
			sufixes: ["Sufixes", "Station", "Mart"],
			domains: []
		};
	},
	methods: {
		addPrefix(prefix) {
			this.prefixes.push(prefix);
			this.prefix = "";
		},
		addSufix(sufix) {
			this.sufixes.push(sufix);
			this.sufix = "";
		},
		generate() {
			const domains = [];
			for (const prefix of this.prefixes) {
				for (const sufix of this.sufixes) {
					domains.push(prefix + sufix);
        }
      }
      return domains;
		},
		removePrefix(prefix) {
			this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
		},
		removeSufix(sufix) {
			this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
		}
	},
  created() {
    this.domains = this.generate()
  }
};
</script>
<style>
#slogan {
  margin-top: 30px;
  margin-bottom: 30px;
}
#main {
  background-color: #f1f1f1;
  padding-top: 30px;
  padding-bottom: 30px;
}
</style>
