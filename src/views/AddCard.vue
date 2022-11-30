<template>
  <div class="home">
    <CustomButton :text="'X'" :color="'#8f0707'" @buttonClick="deleteCard"/>
    <div class="cardContainer">
      <p class="title">
        {{ itemId }}
      </p>
    </div>
  </div>
</template>

<script>
import CustomButton from "@/components/customButton";

export default {
  name: 'AddCard',
  props: {
    itemId: {
      type: Number,
      required: true,
    },
  },
  methods: {
    deleteCard() {
      this.$emit('deleteCard', this.itemId)
    },
  },
  components: {
    CustomButton
  },


}
</script>

<style lang="scss" scoped>
.home{
  width: 25%;
  padding: 2rem 8rem;
}
.cardContainer{
  border: 2px solid black;
  width: 300px;
  height: 250px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
