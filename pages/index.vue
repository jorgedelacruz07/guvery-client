<template>
  <v-app>
    <Navbar></Navbar>
    <v-container grid-list-md text-xs-center>
      <v-layout row wrap>
        <v-flex xs12 sm6 offset-sm3>
          <v-container fluid grid-list-md>
            <v-layout row wrap>
              <v-flex xs12>
                <v-card>
                  <v-card-text>
                    <v-form ref="form" lazy-validation>
                      <v-text-field
                      v-model="domain"
                      :rules="urlRules"
                      label="Dominio"
                      required
                      ></v-text-field>
                      <v-btn
                      @click="getProduct"
                      >Enviar</v-btn>
                    </v-form>
                  </v-card-text>
                </v-card>
              </v-flex>
              <v-flex xs12 class="mt-4" v-if="product.title" :key="product.title">
                <v-card class="">
                  <v-card-media
                  :src="product.image"
                  height="125px"
                  contain
                  ></v-card-media>
                  <v-card-title primary-title>
                    <div>
                      <h3 class="headline mb-0">{{ product.title }}</h3>
                      <div class="body-2 mt-3">Precio: {{ product.price }}</div>
                    </div>
                  </v-card-title>
                </v-card>
              </v-flex>
              <v-flex xs12 v-else>
                <v-card>
                  <v-card-text>
                    <p class="text-xs-center title">
                      No se encontró producto
                    </p>
                  </v-card-text>
                </v-card>
              </v-flex>
            </v-layout>
          </v-container>
        </v-flex>
      </v-layout>
    </v-container>
  </v-app>
</template>

<script>
import Navbar from '../layouts/Navbar'
const cheerio = require('cheerio')

export default {
  data () {
    return {
      product: {},
      domain: '',
      urlRules: [
        v => !!v || 'Dominio requerido'
        // v => /^[a-zA-Z0-9][a-zA-Z0-9-]{1,61}[a-zA-Z0-9]\.[a-zA-Z]{2,}$/.test(v) || 'Dominio inválido'
      ]
    }
  },
  watch: {
    domain: function (v) {
      this.domain = v.toLowerCase().trim()
    }
  },
  methods: {
    async getProduct () {
      try {
        const p = await this.$axios.$get('/scrape?url=' + this.domain)
        console.log(p)
        this.product = p
      } catch (e) {
        this.product = {}
      }
    }
  },
  components: {
    Navbar
  }
}
</script>

<style>
  .card-article {
    height: 200px !important;
  }
</style>
