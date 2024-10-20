<template>
  <div>
    <h2>Resume</h2>
    <iframe :src="resume" type="application/pdf"></iframe>
  </div>
</template>
  
  <script>
import pdf from "../assets/kevin-engel-resume-10-20.pdf";

export default {
  data() {
    return {
      resume: pdf,
    };
  },
};
</script>
  
  
<style>
iframe {
  width: 100%;
  height: 80vh;
}
</style>