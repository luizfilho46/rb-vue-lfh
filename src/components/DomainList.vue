<template>
  <div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <app-item-list title="Prefixos" type="prefix" v-bind:items="items.prefix" v-on:addItem="addItem" v-on:removeItem="removeItem"></app-item-list>
          </div>
          <div class="col-md">
            <app-item-list title="Sufixos" type="sufix" v-bind:items="items.sufix" v-on:addItem="addItem" v-on:removeItem="removeItem"></app-item-list>
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
                  <div class="col-md-6">
                    {{ domain.name }}
                  </div>
                  <div class="col-md-3">
                    <span class="badge badge-info">{{ domain.available ? 'Disponível' : 'Não Dispinível' }}</span>
                  </div>
                  <div class="col-md-3 text-right">
                    <a class="btn btn-info" v-bind:href="domain.checkout" target="_blank">
                      <span class="fa fa-shopping-cart">
                      </span>
                    </a>
                    &nbsp;
                    <button class="btn btn-info" @click="openDomain(domain)">
                      <span class="fa fa-search"></span>
                    </button>
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
 import AppItemList from './AppItemList';

export default {
  name: "app",
  components: {
    AppItemList
  },
	data: function() {
		return {};
	},
	methods: {
		addItem(item) {
      this.$store.dispatch("addItem", item)
		},
		removeItem(item) {
      this.$store.dispatch("removeItem", item)
		},
    getItems (type) {
      this.$store.dispatch("getItems", type)
    },
    generateDomains () {
      this.$store.dispatch("generateDomains")
    },
    openDomain(domain) {
      this.$router.push({
        path: `/domains/${domain.name}`
      })
    }
  },
  computed: {
    items() {
      return this.$store.state.items
    },
    domains() {
      return this.$store.state.domains
    }
  },
  created () {
    Promise.all([
        this.getItems("prefix"),
        this.getItems("sufix")
    ]).then(() => {
      this.generateDomains()
    })
  }
};
</script>
<style>

</style>
