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
            <button class="card__btn" @click="increment">Клик</button>
        </div>
        <button class="card__btn__del" @click="removeItem">Удалить</button>
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

.card__btn {
    width: 100px;
    height: 30px;
}

.card__btn__del {
    width: 100px;
    height: 30px;
}
</style>