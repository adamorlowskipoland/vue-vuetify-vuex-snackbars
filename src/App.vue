<template>
  <v-app>

    <v-toolbar fixed app>
      <v-toolbar-title>Snackbar Demo</v-toolbar-title>
    </v-toolbar>

    <v-content>
      <v-container fluid>
        <v-slide-y-transition mode="out-in">
          <v-layout column align-center>
            <snackbar-store/>
            <v-snackbar
              :text="text"
              :timeout="timeout"
              :top="y === 'top'"
              :bottom="y === 'bottom'"
              :left="x ==='left'"
              :right="x === 'right'"
              :multi-line="mode === 'multi-line'"
              :vertical="mode === 'vertical'"
              v-model="snackbar">
              {{text}}
              <v-btn flat dark @click="snackbar = false">
                Close
              </v-btn>
            </v-snackbar>
            <router-view v-on:showSnackbar="showSnackbar"/>
          </v-layout>
        </v-slide-y-transition>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
  import snackbarStore from '@/components/SnackbarStore'

  export default {
    components: {
      snackbarStore
    },
    data () {
      return {
        snackbar: false,
        text: '',
        timeout: null,
        y: 'top',
        x: null,
        mode: null
      }
    },
    methods: {
      showSnackbar (text, timeout = 3000, yPos = 'top', xPos, mode) {
        this.text = text
        this.timeout = timeout
        this.y = yPos
        this.x = xPos
        this.mode = mode
        this.snackbar = true
      }
    }
  }
</script>
