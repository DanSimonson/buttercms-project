<script>
  //const butter = Butter('34d3d54d8f742ba36133328ca6b67a50a85ddfe1');
  import butter from '@/buttercms';
  //import { butter } from '@/buttercms'
  //var butter = Butter('34d3d54d8f742ba36133328ca6b67a50a85ddfe1');
  export default {
    name: 'customer-page',
    data() {
      return {
        page: {
          fields: {}
        }
      }
    },
    methods: {
      getPage() {
        butter.page.retrieve('*', 'homepage')
          .then((res) => {
            console.log(res.data.data)
            this.page = res.data.data
          }).catch((res) => {
            console.log(res)
          })
      }
    },
    created() {
      this.getPage()
    }
  }
</script>

<template>
  <div id="customer-page">
    <figure>
      <img :src="page.fields.hero_image">
    </figure>
    <h1>{{ page.fields.headline }}</h1>
    <button>{{ page.fields.call_to_action }}</button>

    <h3>Customers Love Us!</h3>
    <!-- Loop over customer logos -->
    <img v-for="logo in page.fields.customer_logos" :src="logo.logo_image">
  </div>
</template>



<style scoped>
</style>