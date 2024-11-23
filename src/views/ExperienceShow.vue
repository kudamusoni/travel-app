<template>
    <section v-if="destination">
        <h1>{{ experience.name }}</h1>
        <img :src="`/images/${experience.image}`" :alt="experience.name">
        <p>{{ experience.description }}</p>
    </section>
</template>

<script>
export default {
    props: {
        id: {
            type: Number,
            required: true
        },
        experienceSlug: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            destination: null
        }
    },
    computed: {
        experience() {
            return this.destination.experiences.find(
                experience => experience.slug === this.experienceSlug
            )
        }
    },
    methods: {
        async loadData() {
            const response = await fetch(`/api/${this.$route.params.slug}.json`)
            this.destination = await response.json()
        }
    },
    async created() {
        this.loadData()
        // this.$watch(() => this.$route.params, this.loadData);
    },
}
</script>