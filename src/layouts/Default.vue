<template>
  <div>
    <slot />
    <footer class="footer"></footer>
  </div>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<style>
#app {
  display: flex;
  flex-direction: column;
  height: 100%;
  justify-content: center;
  align-content: center;
}

html,
body {
  overflow-x: hidden;
  min-height: 10000px;
  height: 100%;
}

body {
  font-family: -apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", Roboto,
    "Helvetica Neue", Arial, sans-serif;
  margin: 0;
  padding: 0;
  line-height: 1.5;
}
</style>
