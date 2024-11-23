<template>
    <div v-if="destination">
        <section class="destination" >
            <h1>{{ destination.name }}</h1>
            <GoBack />
            <div class="destination-details">
                <img :src="`/images/${destination.image}`" :alt="destination.name">
                <p>{{ destination.description }}</p>
            </div>
        </section>

        <section class="experiences">
            <h2>Top Experiences in {{ destination.name }}</h2>
            <div class="cards">
                <router-link
                    v-for="experience in destination.experiences"
                    :key="experience.slug"
                    :to="{name: 'experience.show', params:{experienceSlug: experience.slug}}"
                >
                    <ExperienceCard 
                        :experience="experience"/>
                </router-link>
            </div>
            <router-view />
        </section>
    </div>
</template>

<script>
import ExperienceCard from "../components/ExperienceCard.vue";
import GoBack from "../components/GoBack.vue";
export default {
    components: {ExperienceCard,GoBack},
    props: {
        id: {
            type: Number,
            required: true
        }
    },
    data() {
        return {
            destination: null
        }
    },
    computed: {
    },
    methods: {
        async loadData() {
            const response = await fetch(`/api/${this.$route.params.slug}.json`)
            this.destination = await response.json()

            console.log(this.destination);
        }
    },
    async created() {
        this.loadData()
        // this.$watch(() => this.$route.params, this.loadData);
        console.log(this.$route.params);
    }
}
</script>