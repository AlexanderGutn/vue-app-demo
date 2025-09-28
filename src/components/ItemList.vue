<script>
import ItemCard from './ItemCard.vue';
import ItemEditor from './ItemEditor.vue';

export default {
  components: {
    ItemCard,
    ItemEditor
  },
  data() {
    return {
      items: [
        {title: "Карточка 1", description: "Описание карточки 1"},
        {title: "Карточка 2", description: "Описание карточки 2"},
        {title: "Карточка 3", description: "Описание карточки 3"}
      ], 
      sumClick: 0,
      maxId: 3,
      editingIndex: null,
      editingDraft: null,
      showEditor: false
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
    },
    openEditor(index) {
        this.editingIndex = index
        this.editingDraft = { title: this.items[index].title, description: this.items[index].description }
        this.showEditor = true
    },
    saveEdit(updated) {
        const i = this.editingIndex
        if (i != null) {
          this.items[i] = { ...this.items[i], ...updated } // обновляем title/description, сохраняем count
        }
        this.closeEditor()
    },
    closeEditor() {
        this.showEditor = false
        this.editingIndex = null
        this.editingDraft = null
    }
  }
}
</script>

<template>
  <div class="item-list">
    <button @click="addItem" class="btn">Добавить карточку</button>
    <button @click="delAll" class="btn">Удалить все</button>
    <p>Кол-во карточек: {{ countCard }}</p>
    <p>Кол-во кликов по карточкам всего: {{ sumClick }}</p>
    <p>Список карточек:</p>
    
    <div v-if="showEditor" class="modal">
      <ItemEditor
        :model-value="editingDraft"
        @save="saveEdit"
        @cancel="closeEditor"
      />
    </div>

    <ItemCard
      v-for="(item, index) in items"
      :key="index"
      :title="item.title"
      :description="item.description"
      @clicked="incrementSum"     
      @removeItem="delItem(index)"
      @edit="openEditor(index)"      
    />
  </div>

</template>

<style scoped>
  .item-list {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    margin-left: 30px;
  }

  .btn {
      width: 150px;
      height: 30px;
      margin-top: 10px;
  } 
</style>