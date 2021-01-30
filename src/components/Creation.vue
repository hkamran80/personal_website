<template>
    <div>
        <v-card class="mx-auto" outlined>
            <v-card-title>
                <v-row no-gutters>
                    <v-col class="text-wrap--break" v-text="creation.name" />
                    <v-col cols="4" class="text-right">
                        <v-btn icon v-if="creation.cancelled">
                            <v-icon color="primary">
                                mdi-puzzle-remove-outline
                            </v-icon>
                        </v-btn>
                        <v-btn
                            icon
                            v-if="
                                Object.keys(creation.contributors).length !== 0
                            "
                            @click="creation.dialogs.contributors = true"
                        >
                            <v-icon color="primary">
                                mdi-account-multiple-outline
                            </v-icon>
                        </v-btn>
                        <v-btn
                            icon
                            v-if="creation.repository"
                            :href="creation.repository"
                        >
                            <v-icon color="primary">mdi-github</v-icon>
                        </v-btn>
                        <v-btn icon v-if="creation.site" :href="creation.site">
                            <v-icon color="primary">mdi-web</v-icon>
                        </v-btn>
                    </v-col>
                </v-row>
            </v-card-title>
            <v-card-subtitle v-text="creation.status" />
            <v-card-text v-text="creation.description" />
        </v-card>
        <v-dialog
            v-model="creation.dialogs.contributors"
            v-if="Object.keys(creation.contributors).length !== 0"
            width="500"
        >
            <v-card>
                <v-card-title> {{ creation.name }}: Contributors </v-card-title>
                <v-card-text>
                    <v-list>
                        <v-list-item
                            v-for="(collaborator,
                            name) in creation.contributors"
                            :key="name"
                            :three-line="collaborator.role.length > 56"
                        >
                            <v-list-item-content>
                                <v-list-item-title
                                    v-text="name"
                                ></v-list-item-title>
                                <v-list-item-subtitle
                                    v-text="collaborator.role"
                                ></v-list-item-subtitle>
                            </v-list-item-content>

                            <v-list-item-icon
                                @click="
                                    open_link(collaborator.link.url, creation)
                                "
                                :title="collaborator.link.url"
                            >
                                <v-btn icon>
                                    <!-- TODO: Fix the color for the Medium icon -->
                                    <v-icon
                                        color="primary"
                                        v-text="collaborator.link.icon"
                                    ></v-icon>
                                </v-btn>
                            </v-list-item-icon>
                        </v-list-item>
                    </v-list>
                </v-card-text>
            </v-card>
        </v-dialog>
    </div>
</template>

<script>
export default {
    name: "Creation",
    props: {
        creation: Object
    }
};
</script>

<style></style>