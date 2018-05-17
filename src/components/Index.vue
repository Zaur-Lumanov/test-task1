<template lang="pug">
	
</template>

<script>
export default {
  name: "Index",
  data() {
    if (!localStorage.login) {
      this.$router.push("login");
    } else {
      this.$router.push("main");
    }

    return {};
  }
};
</script>
