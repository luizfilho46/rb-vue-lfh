<template>
    <div>
        {{ domain }}
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
            console.log(this.$route.params)
        }
    }
</script>