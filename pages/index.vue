<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card class="logo py-4 d-flex justify-center">
        <NuxtLogo />
        <VuetifyLogo />
      </v-card>
      <v-card>
        <v-card-title class="headline">
          Welcome to the Vuetify + Nuxt.js template
        </v-card-title>
        <v-data-table
          :headers="starWarsHeaders"
          :items="starWarsVehicle"
        >
        </v-data-table>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            nuxt
            to="/inspire"
          >
            Continue
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import getStarWarsVehicles from './query.gql'

export default {
  data() {
    return {
      starWarsHeaders: [
        { text: 'Name', align: 'start', value: 'name' },
        { text: 'Model', value: 'model' },
        { text: 'Max Atmosphering Speed', value: 'maxAtmospheringSpeed' },
        { text: 'Passengers', value: 'passengers' },
        { text: 'Length', value: 'length' },
      ],
      starWarsVehicle: [],
      starWarsLoadingData: true,
    }
  },
  apollo: {
    starWarsVehicle: {
      query: getStarWarsVehicles,
      result() {
        this.starWarsLoadingData = false
      },
      update(data) {
        return data.allVehicles.vehicles
      },
    },
  }
}
</script>