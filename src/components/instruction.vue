<template>
  <div id="instructionContainer">
    <h1>instruction</h1>

    <div class="card_actions_instruction">
      <p>Press The "Add Card" button to add the new Card</p>
      <p>Use the "Sort Card" button to sort the cards by the increase.</p>

      <p>Press an X Icon on the top Right to delete them</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "instructions",
  data() {
    return {

    }
  }
}

</script>

<style lang="scss" scoped>
#instructionContainer{
  width: 350px;
  height: 100%;
  border-left: 1px solid black;
  position: absolute;
  right: 0;
  top: 0;
  background-color: silver;

  .card_actions_instruction{
    margin-top: 15rem;
    p{
      font-weight: 600;
    }
  }
}
</style>
