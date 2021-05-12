<template>
    <v-container class="d-flex justify-space-between flex-column flex-grow-1">
        <div class="mt-n4">
            <h6 class="text-h6 pb-4">Instalacion completada!</h6>

            <div class="text-body-1" v-if="$root.$data.release !== null">
                <p>
                    Felicitaciones!
                    {{ getDeviceName($root.$data.product) }} esta corriendo LineageOS 18.1
                </p>
            </div>
        </div>

        <div class="d-flex justify-space-between">
            <v-btn text @click="$bubble('prevStep')">Back</v-btn>
        </div>
    </v-container>
</template>

<style>
.theme--light.v-sheet--outlined {
    border-width: 2px;
}

.theme--light.v-sheet--outlined.v-card--p-highlight {
    border: 2px solid #007cfa !important;
}
</style>

<script>
import { getDeviceName } from "../core/devices";

export default {
    name: "FinishStep",

    props: ["device", "blobStore", "active"],

    watch: {
        active: async function (newState) {
            if (newState) {
                this.saEvent("step_finish");
            }
        },
    },

    methods: {
        getDeviceName,
    },
};
</script>
