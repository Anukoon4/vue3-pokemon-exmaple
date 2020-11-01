<template>
  <div class="card">
    <div class="title">
      <slot name="title"/>
      </div>
    <div class="content">
       <slot name="image"/>
    </div>
    <div class="description">
        <slot name="description"/>
    </div>
  </div>
</template>s

<script>
export default {

}
</script>

<style scoped>
.card {
  border: 1px splid silver;
  border-radius: 8px;
  max-width: 200px;
  box-shadow: 0px 1px 3px darkgray;
  margin: 0 5px;
  transition: 0.2;
}


.title,
.content,
.description {
  padding: 16px;
  text-transform: capitalize;
  text-align: center;
}
.title,
.content {
  border-bottom: 1px solid silver;
}
</style>
