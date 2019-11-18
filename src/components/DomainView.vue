<template>
    <div>
        <div class="text-center">
            <h2>{{ domain }}</h2>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                domain: ""
            }
        },
        created() {
            this.domain = this.$route.params.domain
        }
    }
</script>