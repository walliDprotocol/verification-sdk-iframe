<template>
  <v-container class="connect-account pa-3">
    <v-row class="text-center">
      <v-col cols="12" class="d-flex">
        <v-col cols="auto" class="d-flex align-center">
          <v-img
            :src="`./logos/${selectedAccount.IdName}.webp`"
            contain
            max-height="40"
            max-width="40"
          />
        </v-col>
        <v-col
          cols="8"
          class="pl-0 d-flex flex-column align-start justify-center"
        >
          <p class="bold-text-p text-uppercase mb-0">
            {{ selectedAccount.IdNameDesc }}
          </p>
          <p class="mb-0">
            {{ userData.username }}
          </p>
          <p class="bold-text-p mb-0">
            {{ userData.name }}
          </p>
        </v-col>
        <v-spacer />

        <v-col cols="2" class="d-flex flex-column align-center justify-center">
          <p
            class="bold-text-p text-uppercase mb-0"
            :style="{
              cursor: 'pointer',
              color: allSelected ? '#01022E' : '#00AFC5',
            }"
            @click="setAll"
          >
            {{ allSelected ? "Selected!" : "Select all" }}
          </p>
        </v-col>
      </v-col>
    </v-row>

    <v-row
      class="text-center"
      v-for="(item, index) in selectedAccount.options"
      :key="index"
    >
      <v-col cols="12" class="d-flex align-start">
        <v-col cols="2" class="d-flex fill-height align-start">
          <p class="bold-text-p text-left mb-0">
            {{ item.field }}
          </p>
        </v-col>
        <v-col
          cols="5"
          class="pl-0 d-flex fill-height flex-column align-start justify-space-between"
        >
          <p
            class="normal-text-p text-left"
            v-for="(desc, index) in item.description"
            :key="index"
          >
            {{ desc }}
          </p>
        </v-col>
        <v-spacer />
        <v-col
          cols="2"
          class="d-flex fill-height flex-column align-center justify-center py-4"
        >
          <v-switch
            class="mt-0 form-switch"
            v-model="item.state"
            hide-details
            :ripple="false"
          ></v-switch>
        </v-col>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "HelloWorld",
  props: ["selectedAccount"],
  computed: {
    allSelected() {
      return this.selectedAccount?.options.every((e) => e.state);
    },
    userData() {
      return this.selectedAccount?.userData || {};
    },
  },
  methods: {
    setAll() {
      if (this.allSelected) {
        this.selectedAccount?.options.map((e) => (e.state = false));
      } else {
        this.selectedAccount?.options.map((e) => (e.state = true));
      }
    },
  },
  data() {
    return {
      selected: -1,
    };
  },
};
</script>
<style lang="scss"></style>
