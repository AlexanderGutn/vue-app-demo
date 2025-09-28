<script>
export default {
  name: "ItemEditor",
  props: {
    modelValue: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      draft: { ...this.modelValue }
    }
  },
  watch: {
    modelValue(newVal) { this.draft = { ...newVal } }
  },
  emits: ['save','cancel'],
  methods: {
    onSave()   { this.$emit('save', { ...this.draft }) },
    onCancel() { this.$emit('cancel') }
  }
}
</script>

<template>
  <div class="editor">
    <label>
      Title
      <input v-model="draft.title" type="text" />
    </label>
    <label>
      Description
      <input v-model="draft.description" type="text" />
    </label>
    <div class="row">
      <button @click="onSave">Сохранить</button>
      <button @click="onCancel">Отмена</button>
    </div>
  </div>
</template>

<style scoped>
    .editor {
        display:flex;
        flex-direction:column;
        gap:8px;
        padding:12px;
        border:1px solid #e2e8f0;
        border-radius:8px;
        background:#fff; }
    .row {
        display:flex;
        gap:8px; }
</style>
