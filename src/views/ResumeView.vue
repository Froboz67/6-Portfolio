<template>
  <div>
    <h2>Resume View</h2>
    <embed :src="resume" />
  </div>
</template>
  
  <script>
import pdf from "../assets/kevin_engel_resume.pdf";

export default {
  data() {
    return {
      resume: pdf,
    };
  },
};
</script>
  
  
<style>
embed {
  width: 100%;
  height: 80vh;
}
</style>