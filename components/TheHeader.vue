<template>
  <div>
    <b-navbar type="dark" id="navbar" class="rounded p-2">
      <nuxt-link to="/">
        <b-navbar-brand class="ml-4">Nuxt Blog</b-navbar-brand>
      </nuxt-link>
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav class="mx-auto">
          <AppSearchInput />
        </b-navbar-nav>
        <b-navbar-nav>
          <b-nav-item to="/">Home</b-nav-item>
        </b-navbar-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown right>
            <!-- Using 'button-content' slot -->
            <template #button-content>
              <em>User</em>
            </template>
            <b-dropdown-item href="#">Profile</b-dropdown-item>
            <b-dropdown-item href="#">Log Out</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
#navbar {
  background-image: linear-gradient(
      280deg,
      #3252d8 52%,
      rgba(0, 224, 255, 0.82)
    ),
    linear-gradient(to bottom, #3252d8, #3252d8);
}
</style>