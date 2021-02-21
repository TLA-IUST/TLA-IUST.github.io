<template>
  <v-row justify="center" align="center">
    <v-col lg="1" xl="1" cols="0"/>
    <v-col lg="10" xl="10" cols="12" class="justify-center">

      <div class="yellow lighten-3 elevation-6 pa-2">
        <div class="pa-5">
          <div class="d-flex align-center justify-center">
            <v-img :src="LOGO" max-width="100"/>
          </div>
          <div :class="`text-center ${textSize.courseTitle} pa-2`">{{course.title}}</div>
        </div>


        <div v-if="isMainMenuVisible"
             class="d-flex align-center justify-center">

          <v-btn
            v-for="(item, index) in menu"
            :key="index"
            color="black"
            v-ripple="{ class: `light-blue--text` }"
            :style="page===item.pageName ? 'background-color: #B3E5FC' : ''"
            @click="page=item.pageName"
            tile
            text
            large>
            {{item.text}}
            <v-icon class="ml-2">{{item.icon}}</v-icon>
          </v-btn>

        </div>
      </div>

      <div class="pa-2">
        <about v-show="page===HOME_PAGE" :people="people" :course-description="course.description"/>
        <Schedule v-show="page===SCHEDULE_PAGE" :events="schedule.events"/>
        <Assignments v-show="page===ASSIGNMENT_PAGE" :assignments="assignments"/>
        <Assignments v-show="page===PROJECT_PAGE" :assignments="projects"/>
        <CourseMaterials v-show="page===COURSE_MATERIAL_PAGE" :materials="materials"/>
      </div>

      <div v-if="!isMainMenuVisible" class="bottom-nav">
        <v-bottom-navigation
          v-model="value"
          color="blue">

          <v-btn v-for="(item, index) in bottomNavigationMenu" :key="index" @click="page=item.pageName">
            <span class="text-caption pt-1">{{item.text}}</span>
            <v-icon>{{item.icon}}</v-icon>
          </v-btn>


        </v-bottom-navigation>
      </div>

    </v-col>
    <v-col lg="1" xl="1" cols="0"/>
  </v-row>
</template>

<script>

  import About from "../components/About";
  import Footer from "../components/Footer";
  import CourseMaterials from "../components/CourseMaterials";
  import Assignments from "../components/Assignments";
  import Schedule from "../components/Schedule";

  const HOME_PAGE = 'home';
  const SCHEDULE_PAGE = 'schedule';
  const ASSIGNMENT_PAGE = 'assignments';
  const PROJECT_PAGE = 'projects';
  const COURSE_MATERIAL_PAGE = 'materials';

  // Site Images
  const LOGO = require('../static/images/iust.png');

  // Profile images
  const MALE_PROFILE = require('../static/images/profile-boy.jpg');
  const FEMALE_PROFILE = require('../static/images/profile-girl.jpg');
  const REZA_ENTEZARI = require('../static/images/Entezari.jpg');
  const DANI_BAZI = require('../static/images/danial.jpg');
  const ALI_SEDGHI = require('../static/images/ali.jpg');
  const AMIN_GHASVARI = require('../static/images/amin.png');
  const ARMAN_HEYDARI = require('../static/images/arman.jpg');
  const ZAHRA_HOSSEINI = require('../static/images/zahra.jpg');
  const AMIR_ALI_PAKDAMAN = require('../static/images/amirali.jpg');
  const YASAMIN_MADANI = require('../static/images/yasamin.jpg');

  // Resources Covers
  const PETER_LINZ = require('../static/images/Peter Linz.jpg');
  const MICHAEL_SIPSER = require('../static/images/Michael Sipser.jpg');
  const FILE_PETER_LINZ = '/_nuxt/static/references/Peter Linz - An Introduction to Formal Languages and Automata [6th ed.]-Jones _ Bartlett (2017).pdf';
  const FILE_MICHAEL_SIPSER = '/_nuxt/static/references/Michael Sipser - Introduction to the Theory of Computation (2012, Thomson South-Western).pdf';

  export default {
    computed: {
      HOME_PAGE: () => HOME_PAGE,
      SCHEDULE_PAGE: () => SCHEDULE_PAGE,
      ASSIGNMENT_PAGE: () => ASSIGNMENT_PAGE,
      PROJECT_PAGE: () => PROJECT_PAGE,
      COURSE_MATERIAL_PAGE: () => COURSE_MATERIAL_PAGE,
      // Images
      LOGO: () => LOGO,
      isMainMenuVisible() {
        switch (this.$vuetify.breakpoint.name) {
          case 'xs':
            return false;
          case 'sm':
            return false;
          case 'md':
            return true;
          case 'lg':
            return true;
          case 'xl':
            return true;
        }
      },
      textSize() {
        switch (this.$vuetify.breakpoint.name) {
          case 'xs':
            return {
              courseTitle: 'text-h4',
              courseDescription: 'text-h8',
            };
          case 'sm':
            return {
              courseTitle: 'text-h2',
              courseDescription: 'text-h6',
            };
          case 'md':
            return {
              courseTitle: 'text-h2',
              courseDescription: 'text-h4',
            };
          case 'lg':
            return {
              courseTitle: 'text-h2',
              courseDescription: 'text-h4',
            };
          case 'xl':
            return {
              courseTitle: 'text-h2',
              courseDescription: 'text-h4',
            };
        }
      }
    },
    data: () => ({
      page: HOME_PAGE,
      value: -1,
      // Course Details
      course: {
        title: "Automata Theory",
        subtitle: "1399-1400",
        description: "The theory of computation includes several topics: automata theory, formal languages and grammars, computability, and complexity. Together, this material constitutes the theoretical foundation of computer science. Loosely speaking we can think of automata, grammars, and computability as the study of what can be done by computers in principle, while complexity addresses what can be done in practice...",
      },

      // Main Menu
      menu: [
        {
          pageName: HOME_PAGE,
          text: "Home",
          icon: 'mdi-home'
        },
        {
          pageName: SCHEDULE_PAGE,
          text: "Schedule",
          icon: 'mdi-calendar'
        },
        {
          pageName: ASSIGNMENT_PAGE,
          text: "Assignments",
          icon: 'mdi-book-open'
        },
        {
          pageName: PROJECT_PAGE,
          text: "Projects",
          icon: 'mdi-rocket'
        },
        {
          pageName: COURSE_MATERIAL_PAGE,
          text: "Resources",
          icon: 'mdi-book'
        },
      ],

      // Bottom Navigation
      bottomNavigationMenu: [
        {
          pageName: SCHEDULE_PAGE,
          text: "Schedule",
          icon: 'mdi-calendar'
        },
        {
          pageName: ASSIGNMENT_PAGE,
          text: "Assignments",
          icon: 'mdi-book-open'
        },
        {
          pageName: PROJECT_PAGE,
          text: "Projects",
          icon: 'mdi-rocket'
        },
        {
          pageName: COURSE_MATERIAL_PAGE,
          text: "References",
          icon: 'mdi-book'
        },
      ],

      // Schedule
      schedule: {
        events: [
          {
            name: 'Introduction',
            start: '2021-02-25 18:00',
            end: '2021-02-25 20:00',
            color: 'red'
          },
          // {
          //   name: 'Introduction',
          //   start: '2021-02-01 9:00',
          //   end: '2021-02-09 9:00',
          //   color: 'red'
          // },
          // {
          //   name: 'Introduction',
          //   start: '2021-02-01 9:00',
          //   end: '2021-02-09 9:00',
          //   color: 'red'
          // },
        ]
      },

      // Assignments
      assignments: [
        // {
        //   name: "Assignment number 1",
        //   file: ''
        // },
        // {
        //   name: "Assignment number 2",
        //   file: ''
        // },
        // {
        //   name: "Assignment number 3",
        //   file: ''
        // },
        // {
        //   name: "Assignment number 4",
        //   file: ''
        // },
        // {
        //   name: "Assignment number 5",
        //   file: ''
        // }
      ],

      // Projects
      projects: [
        // {
        //   name: "Project number 1",
        //   file: ''
        // },
        // {
        //   name: "Project number 2",
        //   file: ''
        // },
        // {
        //   name: "Project number 3",
        //   file: ''
        // }
      ],

      // Characters
      people: {
        professor: {
          name: "M.Reza Entezari",
          image: REZA_ENTEZARI
        },
        assistants: [
          {
            name: "Danial Bazmande",
            image: DANI_BAZI
          }, {
            name: "Arman Heydari",
            image: ARMAN_HEYDARI
          },
          {
            name: "M.Amin Ghasvari",
            image: AMIN_GHASVARI
          },
          {
            name: "Ali Sedaghi",
            image: ALI_SEDGHI
          },
          {
            name: "Mahsa Ghaderan",
            image: FEMALE_PROFILE
          },
          {
            name: "Zahra Hosseini",
            image: ZAHRA_HOSSEINI
          },
          {
            name: "Yasamin Madani",
            image: YASAMIN_MADANI
          },
          {
            name: "Amir Ali Pakdaman",
            image: AMIR_ALI_PAKDAMAN
          },
        ],
      },

      // References
      materials: {
        main: [
          {
            name: "An Introduction to Formal Languages and Automata",
            description: "",
            cover: PETER_LINZ,
            file: FILE_PETER_LINZ
          },
          {
            name: "Introduction to the Theory of Computation",
            description: "",
            cover: MICHAEL_SIPSER,
            file: FILE_MICHAEL_SIPSER
          }
        ],
        additional: [
          // {
          //   name: "Reference 1",
          //   description: "This book is Reference 1",
          //   cover: REF_BOOK_2,
          // },
          // {
          //   name: "Reference 2",
          //   description: "This book is Reference 2",
          //   cover: REF_BOOK_1,
          // },
          // {
          //   name: "Reference 3",
          //   description: "This book is Reference 3",
          //   cover: REF_BOOK_2,
          // },
          // {
          //   name: "Reference 4",
          //   description: "This book is Reference 4",
          //   cover: REF_BOOK_1,
          // }
        ]
      }
    }),
    components: { Schedule, CourseMaterials, Footer, About, Assignments },
  }
</script>

<style scoped lang="scss">
  .bottom-nav {
    width: 100%;
    position: fixed;
    bottom: 0;
    left: 0;
    z-index: 2;
  }
</style>