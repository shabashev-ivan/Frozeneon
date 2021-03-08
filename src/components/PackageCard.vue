<template>
  <v-card v-if="value">
    <v-card-title>
      <span class="headline">{{ value.name }}</span>
    </v-card-title>
    <v-list flat>
      <div class="flex justify-start ml-6 mb-4" v-for="item in visibleInfo" :key="item.key">
        <span>{{ item.title }}: </span>
        <span>{{ value[item.key] }}</span>
      </div>
    </v-list>
  </v-card>
</template>

<script>
export default {
  name: "PackageCard",
  props: {
    value: {
      type: Object,
      required: true,
    }
  },
  data() {
    return {
      visibleInfo: [
        {
          title: 'Описание',
          key: 'description',
        },
        {
          title: 'Последняя версия',
          key: 'lastversion',
        },
        {
          title: 'Автор',
          key: 'author',
        },
      ]
    };
  },
}
</script>

<style scoped>

</style>