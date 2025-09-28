<script>
import ItemCard from './ItemCard.vue';

export default {
  components: {
    ItemCard
  },
  data() {
    return {
      items: [
        {title: "Карточка 1", description: "Описание карточки 1"},
        {title: "Карточка 2", description: "Описание карточки 2"},
        {title: "Карточка 3", description: "Описание карточки 3"}
      ], 
      sumClick: 0,
      maxId: 3
    }
  },
  computed: {
    countCard() {
        return this.items.length;
    }
  },
  methods: {
    addItem() {
        this.maxId++;
        this.items.push({            
            title: `Карточка ${this.maxId}`,
            description: `Описание карточки ${this.maxId}`            
        })       
    },
    incrementSum() {
        this.sumClick++;
    },
    delAll () {
        this.items= []
    },
    delItem (index) {        
        this.items.splice(index,1)
    }
  }
}
</script>

<template>
  <div class="item-list">
    <button @click="addItem" class="add-btn">Добавить карточку</button>
    <button @click="delAll" class="del-btn">Удалить все</button>
    <p>Кол-во карточек: {{ countCard }}</p>
    <p>Кол-во кликов по карточкам всего: {{ sumClick }}</p>
    <p>Список карточек:</p>
    <ItemCard
      v-for="(item, index) in items"
      :key="index"
      :title="item.title"
      :description="item.description"
      @clicked="incrementSum"     
      @removeItem="delItem(index)"
      
    />
  </div>
</template>

<style>
.item-list {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-left: 30px;
}
</style>