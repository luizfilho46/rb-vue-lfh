<template>
  <div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <app-item-list title="Prefixos" v-bind:items="items.prefix" v-on:addItem="addPrefix" v-on:removeItem="removePrefix"></app-item-list>
          </div>
          <div class="col-md">
            <app-item-list title="Sufixos" v-bind:items="items.sufix" v-on:addItem="addSufix" v-on:removeItem="removeSufix"></app-item-list>
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
			items: {
        prefix: [],
        sufix: []
      }
		};
	},
	methods: {
		addPrefix(prefix) {
      axios({
        url: "http://localhost:4000",
        method: "post",
        data: {
          query: `
            mutation ($item: ItemInput) {
              newPrefix: saveItem(item: $item) {
                id
                type
                description
              }
            }
          `,
          variables: {
            item: {
              type: 'prefix',
              description: prefix
            }
          }
        }
      }).then( response => {
        const query = response.data
        const newPrefix = query.data.newPrefix
        this.items.prefix.push(newPrefix)
      })
		},
		addSufix(sufix) {
			this.items.sufix.push(sufix);
		},
		removePrefix(prefix) {
			axios({
        url: 'http://localhost:4000',
        method: 'post',
        data: {
          query: `
            mutation ($id: Int) {
              deleted: deleteItem(id: $id) 
            }
          `,
          variables: {
            id: prefix.id
          }
        }
      }).then( () => {
        this.getItems("prefix")
      })
		},
		removeSufix(sufix) {
			this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
    },
    getItems (type) {
      axios({
        url: 'http://localhost:4000',
        method: 'post',
        data: {
          query: `
            query ($type: String) {
              items (type: $type) {
                id
                type
                description
              }
            }

          `,
          variables: {
            type
          }
        }
      }).then( ({ data : { data } }) => {
        this.items[type] = data.items
      })  
    }
  },

  computed: {
    domains() {
			const domains = [];
			for (const prefix of this.items.prefix) {
				for (const sufix of this.items.sufix) {
          const name = prefix.description + sufix.description;
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
    this.getItems("prefix")
    this.getItems("sufix")
  }
};
</script>
<style>

</style>
