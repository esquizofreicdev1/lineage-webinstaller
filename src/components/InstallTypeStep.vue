<template>
    <v-container class="d-flex justify-space-between flex-column flex-grow-1">
        <div class="mt-n4">
            <h6 class="text-h6 pb-4">Seleccione un tipo de instalacion</h6>

            <div class="text-body-1">
                <p>
                    El instalador le puede ayudar a instalar una compilacion de LineageOS de forma facil y rapida!
                </p>
            </div>
        </div>

        <div class="d-flex flex-wrap justify-space-around">
            <v-card
                outlined
                max-width="16rem"
                class="ma-4 d-flex flex-column"
                ripple
                :color="
                    $root.$data.installType === 'clean'
                        ? 'grey lighten-4'
                        : null
                "
                :class="
                    $root.$data.installType === 'clean'
                        ? 'v-card--selected'
                        : null
                "
                @click="setType('clean')"
            >
                <v-card-title class="mt-n2">
                    <v-icon class="pr-2 py-2" color="rgba(0, 0, 0, 0.87)"
                        >mdi-cellphone-erase</v-icon
                    >
                    Instalacion limpia</v-card-title
                >
                <v-card-subtitle
                    >Cambiar su rom por LineageOS 18.1
                    <strong class="red--text text--darken-2"
                        >Los datos de su dispositivo seran borrados!</strong
                    >
                </v-card-subtitle>
            </v-card>

            <v-card
                outlined
                max-width="16rem"
                class="ma-4 d-flex flex-column justify-space-between"
                ripple
                :color="
                    $root.$data.installType === 'update'
                        ? 'grey lighten-4'
                        : null
                "
                :class="
                    $root.$data.installType === 'update'
                        ? 'v-card--selected'
                        : null
                "
                @click="setType('update')"
            >
            </v-card>
        </div>

        <div class="d-flex justify-space-between flex-row-reverse">
            <v-btn
                color="primary"
                @click="$bubble('nextStep')"
                :disabled="$root.$data.installType === null"
                >Next <v-icon dark right>mdi-arrow-right</v-icon></v-btn
            >
            <v-btn text @click="$bubble('prevStep')">Back</v-btn>
        </div>
    </v-container>
</template>

<style>
.theme--light.v-sheet--outlined {
    border-width: 2px;
}

.theme--light.v-sheet--outlined.v-card--selected {
    border: 2px solid rgba(0, 0, 0, 0.77) !important;
}
</style>

<script>
export default {
    name: "InstallTypeStep",

    props: ["device", "blobStore", "active"],

    data: () => ({
        firstSet: true,
    }),

    watch: {
        active: async function (newState) {
            if (newState) {
                this.saEvent("step_installtype");
            }
        },
    },

    methods: {
        setType(newType) {
            this.$root.$data.installType = newType;

            if (this.firstSet) {
                this.firstSet = false;
                this.$bubble("nextStep");
            }

            this.saEvent(`install_type__${newType}`);
        },
    },
};
</script>
