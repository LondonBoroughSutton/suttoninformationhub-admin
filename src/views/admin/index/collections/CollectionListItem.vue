<template>
  <li>
    {{ collection.name }}&nbsp;<span
      v-if="auth.isSuperAdmin && !collection.enabled"
      >(disabled)</span
    >&nbsp;
    <gov-link
      v-if="auth.isGlobalAdmin"
      :to="{
        name: editCollectionRoute,
        params: { collection: collection.id },
      }"
    >
      Edit
    </gov-link>
    <br />
    <gov-link @click="$emit('move-up', collection)" v-if="collection.order > 1"
      >(Move up)</gov-link
    >
    <gov-link
      @click="$emit('move-down', collection)"
      v-if="collection.order < collections.length"
      >(Move down)</gov-link
    >
  </li>
</template>

<script>
export default {
  props: {
    collections: {
      type: Array,
      required: true,
    },
    collection: {
      type: Object,
      required: true,
    },
    type: {
      type: String,
      required: true,
      validator: function(value) {
        return ['category', 'persona'].indexOf(value) !== -1
      },
    },
  },

  computed: {
    editCollectionRoute() {
      return this.type === 'category'
        ? 'collections-categories-edit'
        : 'collections-personas-edit'
    },
  },
}
</script>

<style lang="scss" scoped></style>
