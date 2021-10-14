<template>
  <div>
    <JobsList/>
  </div>
</template>

<script>
export default {
  middleware: "isAuthenticated",
  layout: 'AuthReady',
};
</script>
