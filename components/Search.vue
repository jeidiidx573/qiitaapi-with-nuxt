<template>
  <v-form v-model="valid">
    <v-container>
      <v-layout>
        <v-flex xs12 md4>
          <v-text-field
            v-model="firstname"
            :rules="nameRules"
            label="Search!!"
            required
          ></v-text-field>
        </v-flex>
        <v-flex xs12 md4>
          <v-btn color="green" @click="submit"><v-icon>search</v-icon></v-btn>
        </v-flex>
      </v-layout>
    </v-container>
  </v-form>
</template>

<style>
</style>
