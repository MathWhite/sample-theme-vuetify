<template>
  <v-app-bar app>
    <v-app-bar-nav-icon @click="drawer = !drawer" />
    <v-toolbar-title>Doc by Matheus</v-toolbar-title>
    <v-spacer />
    <div class="d-flex align-center">
      <v-switch
        v-model="isDarkTheme"
        @change="toggleTheme"
        class="mt-6 mr-2"
      />
      <v-icon class="ml-2 mr-5">{{ isDarkTheme ? 'mdi-weather-night' : 'mdi-weather-sunny' }}</v-icon>
    </div>
  </v-app-bar>

  <v-navigation-drawer v-model="drawer" app>
    <v-list density="compact" nav>
      <v-list-item
        v-for="item in navItems"
        :key="item.title"
        :to="item.to"
        router
        class="nav-item"
      >
        <v-list-item :prepend-icon="item.icon" :title="item.title"></v-list-item>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
export default {
  data() {
    return {
      drawer: false,
      isDarkTheme: localStorage.getItem('selectedTheme') === 'dark',
      navItems: [
        { title: 'Home', to: '/', icon: 'mdi-home' },
        { title: 'About', to: '/about', icon: 'mdi-information' },
      ],
    };
  },
  methods: {
    toggleTheme() {
      const newTheme = this.isDarkTheme ? 'dark' : 'light';
      this.$vuetify.theme.global.name = newTheme; // Altera o tema global do Vuetify
      localStorage.setItem('selectedTheme', newTheme); // Atualiza o tema no localStorage
    },
  },
  mounted() {
    // Define o tema inicialmente ao montar o componente
    this.$vuetify.theme.global.name = this.isDarkTheme ? 'dark' : 'light';
  },
};
</script>

<style>
.nav-item {
  border-radius: 8px;
  transition: background-color 0.3s ease;
}

.nav-item:hover {
  background-color: var(--v-primary-lighten3);
}

.v-list-item-content {
  display: flex;
  align-items: center;
}

.v-list-item-icon {
  margin-right: 12px; /* Espaço entre ícone e texto */
}
</style>
