<template>
    <div id="nav">
        <AppLink id="logo" to="/">Travel</AppLink>
        <AppLink v-for="destination in destinations" :key="destination.id"
            :to="{ name: 'destination.show', params: {id: destination.id, slug: destination.slug}}">

            <h2>{{ destination.name }}</h2>
        </AppLink>

        <AppLink :to="{name: 'protected'}">Dashboard</AppLink>

        <AppLink to="https://www.youtube.com/watch?v=9YBMYNwKglM">New Cuban</AppLink>
    </div>
</template>

<script>
import sourceData from "../data.json";
export default {
    data() {
        return {
            destinations: sourceData.destinations
        }
    },
}
</script>