<template>
  <div>
    <!-- <h2>Resume</h2> -->
    <iframe :src="resume" type="application/pdf"></iframe>
  </div>
</template>
  
  <script>
import pdf from "../assets/kevin_engel_12_24.pdf";

export default {
  data() {
    return {
      resume: pdf,
    };
  },
};
</script>
  
  
<style>
h2 {
  color: white;
  text-align: center;
}
iframe {
  width: 100%;
  height: 85vh;
}
</style>