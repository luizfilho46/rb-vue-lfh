<template>
  <div>
    <h5>
      {{ title }}
      <span class="badge badge-info">{{ items.length }}</span>
    </h5>
    <div class="card">
      <div class="card-body">
        <ul class="list-group">
          <li class="list-group-item" v-for="item_ in items" v-bind:key="item_.id">
            <div class="row">
              <div class="col=md">{{ item_.description }}</div>
              <div class="col-md text-right">
                <button class="btn btn-info" v-on:click="removeItem(item_)">
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
            v-model="description"
            v-on:keyup.enter="addItem(type, description)"
          />
          <div class="input-group-append">
            <button class="btn btn-info" v-on:click="addItem(type, description)">
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
  props: ["title", "type", "items"],
  data () {
    return {
      description: ""
    }
  },
  methods: {
    addItem(type, description) {
      this.$emit("addItem", {
        type,
        description
      })
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
