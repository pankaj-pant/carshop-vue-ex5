 <template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>carshop with vuetify</span>
      </v-toolbar-title>
    </v-toolbar>

    <v-content>
      <Cars />
    </v-content>
  </v-app>
</template>

<script>
import Cars from './components/Cars';

export default {
  name: 'App',

  components: {
    Cars,
  },

  data: () => ({
    //
  }),
};
</script>
