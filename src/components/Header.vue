<template>
<div>
<b-nav tabs>
   <b-nav-item disabled ><center><h1>Mayor Quiz App</h1></center></b-nav-item>
   <b-nav-item disabled>Counter: {{ numCorrect }}/{{ numTotal }}</b-nav-item>
</b-nav>
</div>
   
</template>
<script>
export default {
   props:[
      "numCorrect",
      "numTotal"
   ]
}
</script>
<style scoped>
.b-nav-item {
   text-align: center;
   font-size: 2rem;
}
</style>