<template>
  <div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <app-item-list title="Prefixos" v-bind:items="prefixes" v-on:addItem="addPrefix" v-on:removeItem="removePrefix"></app-item-list>
          </div>
          <div class="col-md">
            <app-item-list title="Sufixos" v-bind:items="sufixes" v-on:addItem="addSufix" v-on:removeItem="removeSufix"></app-item-list>
          </div>
        </div>
        <br />
        <h5>
          Domínios
          <span class="badge badge-info">{{ domains.length }}</span>
        </h5>
        <div class="card">
          <div class="class-body">
            <ul class="list-group">
              <li class="list-group-item" v-for="domain in domains" v-bind:key="domain.name">
                <div class="row">
                  <div class="col-md">
                    {{ domain.name }}
                  </div>
                  <div class="col-md text-right">
                    <a class="btn btn-info" v-bind:href="domain.checkout" target="_blank">
                      <span class="fa fa-shopping-cart">

                      </span>
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
import axios from "axios/dist/axios";
import AppItemList from './AppItemList';

export default {
  name: "app",
  components: {
    AppItemList
  },
	data: function() {
		return {
			prefixes: [],
			sufixes: []
		};
	},
	methods: {
		addPrefix(prefix) {
			this.prefixes.push(prefix);
		},
		addSufix(sufix) {
			this.sufixes.push(sufix);
		},
		removePrefix(prefix) {
			this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
		},
		removeSufix(sufix) {
			this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
		}
  },

  computed: {
    domains() {
			const domains = [];
			for (const prefix of this.prefixes) {
				for (const sufix of this.sufixes) {
          const name = prefix + sufix;
          const url = name.toLowerCase()
          const checkout = `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com.br`
					domains.push({
            name,
            checkout
          });
        }
      }
      return domains;
    },
  },
  created () {
    axios({
      url: 'http://localhost:4000',
      method: 'post',
      data: {
        query: `
          {
            prefixes {
              id
              type
              description
            }
            sufixes {
              description
            }
          }
        `
      }
    }).then( ({ data : { data } }) => {
      console.log( data )
      // this.prefixes = data.prefixes.map( prefix => prefix.description )
      // this.sufixes = data.sufixes.map( sufix => sufix.description )
    })
  }
};
</script>
<style>

</style>
