<template>
  <v-row justify="center" align="center" class="mt-4">
    <v-col cols="1"/>
    <v-col cols="10" class="justify-center">
      <div :class="`${textSize.title}`">Main Resources</div>
      <v-row class="my-4">
        <v-col
          v-for="(material, index) in materials.main"
          :key="index"
          :cols="materialsColumns">
          <v-card
          height="500">
            <v-img :src="material.cover" height="430"/>
            <v-card-actions class="mt-2">
              <v-spacer/>
              <v-btn text :href="material.file">
                <v-icon class="mr-2" color="green" >mdi-download</v-icon>
                Download
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>


<!--      <div :class="`${textSize.title} mt-8`">Additional Resources</div>-->
      <v-row class="my-4">
        <v-col
          v-for="(material, index) in materials.additional"
          :key="index"
          :cols="materialsColumns">
          <v-card>
            <v-img
              :src="material.cover"/>
            <v-card-title>{{material.name}}</v-card-title>
            <v-card-text>
              <div>{{material.description}}</div>
            </v-card-text>
            <v-card-actions>
              <v-spacer/>
              <v-btn text>
                <v-icon class="mr-2" color="green">mdi-download</v-icon>
                Download
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-col>
    <v-col cols="1"/>
  </v-row>
</template>

<script>
  export default {
    name: "CourseMaterials",
    computed: {
      materialsColumns() {
        switch (this.$vuetify.breakpoint.name) {
          case 'xs':
            return 12;
          case 'sm':
            return 6;
          case 'md':
            return 6;
          case 'lg':
            return 5;
          case 'xl':
            return 4;
        }
      },
      textSize() {
        switch (this.$vuetify.breakpoint.name) {
          case 'xs':
            return {
              title: 'text-h6',
            };
          case 'sm':
            return {
              title: 'text-h6',
            };
          case 'md':
            return {
              title: 'text-h5',
            };
          case 'lg':
            return {
              title: 'text-h5',
            };
          case 'xl':
            return {
              title: 'text-h5',
            };
        }
      }
    },
    props: ['materials']
  }
</script>

<style scoped>

</style>
