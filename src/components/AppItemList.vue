<template>
  <div>
    <h5>
      {{ title }}
      <span class="badge badge-info">{{ items.length }}</span>
    </h5>
    <div class="card">
      <div class="card-body">
        <ul class="list-group">
          <li class="list-group-item" v-for="item_ in items" v-bind:key="item_">
            <div class="row">
              <div class="col=md">{{ item_ }}</div>
              <div class="col-md text-right">
                <button class="btn btn-info" v-on:click="removeItem(item)">
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
            v-model="item"
            v-on:keyup.enter="addItem(item)"
          />
          <div class="input-group-append">
            <button class="btn btn-info" v-on:click="addItem(item)">
              <span class="fa fa-plus"></span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppItemList",
  props: ["title", "items"],
  data () {
    return {
      item: ""
    }
  },
  methods: {
    addItem(item) {
      this.$emit("addItem", item)
      this.item = ""
    },
    removeItem(item) {
      this.$emit("removeItem", item)
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
