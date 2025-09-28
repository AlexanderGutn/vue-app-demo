<script>
export default{
    data() {
        return {
            count: 0
        }
    },
    props: {
        title: {type: String, required: true},
        description: {type: String, required: true}
    },
    methods: {
        increment() {
            this.count++;
            this.$emit("clicked");
        },
        removeItem() {
            this.$emit("removeItem");            
        },
        edit() {
            this.$emit('edit');
        }

    }   
}
</script>

<template>
    <div class="item-card">
        <div>
            <h3 class="card__title">Название: {{ title }}</h3>
            <p class="card__decs">Описание: {{ description }}</p>
            <p class="count__click">Кол-во кликов: {{ count }}</p>
            <button class="btn" @click="increment">Клик</button>
        </div>
        <div class="actions">
             <button class="btn" @click="removeItem">Удалить</button>
             <button class="btn" @click="edit">Редактировать</button>
        </div>   
    </div>
</template>

<style>
.item-card {
    width: 500px;
    height:auto;
    display:flex;
    justify-content: space-between;    
    border: 2px solid;
    border-color: black;
    background-color: rgb(231, 233, 232);
    /* border-radius: 10px; */
    margin-top: 20px;    
    padding: 20px;
}

.actions {
    display:flex;
    flex-direction: column;
}

.btn {
    width: 100px;
    height: 30px;
    margin-top: 10px;
}
</style>