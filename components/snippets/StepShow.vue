<template>
  <div>
    <client-only>
        <vue-mathjax :formula="currentStep"></vue-mathjax>
      </client-only>
  </div>
</template>
<script type="text/javascript">
  export default {
    props: {
      currentStep: {
        required: true,
        type: String
      }
    }
  }
</script>