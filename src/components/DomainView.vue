<template>
    <div>
        <div class="container">
            <div class="text-left">
                <router-link to="/domains">Voltar</router-link>
                <br />
                <br />
                <br />
                <h2>{{ domain }}</h2>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ["domain"],
        data() {
            return {
            }
        },
        created() {
            this.domain = this.$route.params.domain
        }
    }
</script>