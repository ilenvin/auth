<template>
  <div class="text-center" v-if="hideBtn">
    <v-btn  
      class="ma-2"
      outlined
      color="grey lighten-5"
      @click="btnClick()"
    >
    {{ btnText }}
    </v-btn>
  </div>
</template>

<script>
/* eslint-disable */
export default {
    name: 'Button',
    props: {
        hideBtn: { 
            type: Boolean,
            default: true
        },
        btnText: {
            type: String,
            default: () => "Click"
        }
    },
    methods: {
        btnClick() {
            console.log('clicked');
        }
    },
    // data: () => ({
    // })
}
</script>