<template>
  <div id="app">
    <div id="nav">
      <form class="window">
        <customButton text="Create New Card" @buttonClick="formSubmit"/>
      </form>
      <button @click="sort">Sort Cards</button>
    </div>
    <div class="card_content">
      <AddCard v-for="card in filteredData" :item-id="card.id" @deleteCard="deleteCard" />
      <h1 v-if="filteredData.length === 0" class="message">Card is empty You Can Create it</h1>
    </div>
    <instruction />
    <footerSection />
  </div>
</template>

<script>
import AddCard from "@/views/AddCard";
import instruction from "@/components/instruction";
import footerSection from "@/components/footerSection";
import customButton from "./components/customButton";

export default {
  data() {
    return {
      cardData: {

      },
      cards:[
        {
          id: '',
        }
      ]
    }
  },

  methods: {

    deleteCard(itemId) {
      this.cards = this.cards.filter(card => card.id !== itemId)
      this.cards.url.reload()
    },

    sort() {
      console.log('ss')
      this.cards = this.cards.sort(function (a, b) {
        return a.id - b.id
      })
    },

    formSubmit(){
      if(!this.cardData.id){
        this.cards.push({
          id: Math.ceil(Math.random()*1000),
        })
      } else {
        this.cards.forEach(card => {
          if(card.id === this.cardData.id){
            card.title=this.cardData
          }
        })
      }
    },
  },

  created() {
    if (localStorage.cards){
      this.cards = JSON.parse(localStorage.getItem('cards'))
    }else{
      localStorage.cards = JSON.stringify(this.cards)
    }
  },

  watch: {
    cards: {
      handler(val) {
        localStorage.setItem('cards', JSON.stringify(this.cards))
      },
      deep:true
    }
  },

  computed:{
    filteredData(){
      if (this.searchInput) {
        return this.cards.filter(card => {
          return card.title.indexOf(this.searchInput) !== -1 || card.description.indexOf(this.searchInput) !==-1
        })
      } else {
        return this.cards
      }
    },
  },

  components: {
    instruction,
    AddCard,
    footerSection,
    customButton
  },
}
</script>

<style lang="scss">
body{
  margin: 0 auto;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0 auto;
  padding: 0;
  height: 700px;
}

#nav {
  padding: 30px;
  display: flex;
  border-bottom: 1px solid black;
  a {
    font-weight: bold;
    color: #2c3e50;
    margin-left: 20px;
    text-decoration-line: none;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
  button{
    padding: 10px 20px;
    margin-left: 20px;
    outline: none;
    background: none;
    cursor: pointer;
    border: 1px solid black;
    position: unset;
    color: black !important;
    &:hover{
      background-color: black;
      color: white !important;
      transition: 0.3s;
    }
  }
}
.card_content{
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: 0fr;
  grid-column-gap: 0;
  grid-row-gap: 0;
  overflow-y: scroll;
  width: 77%;
  height: inherit;
}
</style>
