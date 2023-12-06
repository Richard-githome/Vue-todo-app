<template>
  <!-- <nav> -->
    <div class="nav-container">
      <div class="nav-header-container">
        <slot name="headerTitle"></slot>
      </div>
      <div class="nav-timer-container">
        <slot name="headerTimer"></slot>
      </div>
    </div>
  <!-- </nav> -->
</template>

<!-- <script>
export default {};
</script> -->

<style scoped>
.nav-container {
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  text-align: center;
  /* margin: 1rem; */
  background-color: var(--appHeaderColor);
  border-radius: 0.375rem;
  box-shadow: 0px 1px 3px .5px rgb(60, 58, 58);
}
.nav-timer-container, .nav-header-container {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  gap: 1rem;
}
.nav-header-container {
  border-bottom: 2px solid var(--colorNotWhite);
  padding-left: .5rem;
}

@media screen and (min-width: 534px) {
  .nav-container {
    display: flex;
    flex-direction: unset;
    align-items: center;
    justify-content: space-between;
    padding: .5rem;
    /* margin: 1rem; */
    background-color: var(--appHeaderColor);
  }
  .nav-header-container {
    border: none;
  }
  /* .nav-header-container {
    display: flex;
    align-items: center;
    justify-content: center;
  } */
  .nav-timer-container {
    display: flex;
    text-align: end;
    justify-content: flex-end ;
  }


}

</style>
