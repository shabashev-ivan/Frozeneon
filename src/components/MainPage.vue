<template>
  <v-container class="mt-16">
    <v-row class="text-center">
      <v-col class="mb-4">
        <v-text-field
            label="Поиск"
            placeholder="Например: vue"
            :error="!!errorText"
            :error-messages="errorText"
            solo
            @input="search"
        />
        <v-data-table
            :headers="headers"
            :items="tableItems"
            :items-per-page="10"
            :loading="searchInProgress"
            class="elevation-1"
            @click:row="openModalForPackage"
        >
          <template #item.homepage="{ value }">
            <a @click.stop target="_blank" :href="value">{{ value }}</a>
          </template>
          <template #item.github="{ value }">
            <a @click.stop target="_blank" :href="value">{{ value }}</a>
          </template>
        </v-data-table>
      </v-col>
    </v-row>
    <v-dialog
        :value="actualNameForModal"
        @click:outside="actualNameForModal = ''"
        width="800px"
    >
      <PackageCard :value="actualPackage"/>
    </v-dialog>
  </v-container>
</template>

<script>
import PackageCard from "@/components/PackageCard";

const unknownError = 'Произошла ошибка, пожалуйста, попробуйте еще раз.'

export default {
  name: 'HelloWorld',
  components: {
    PackageCard
  },
  data() {
    return {
      headers: [
          {
            text: 'Название',
            align: 'start',
            sortable: false,
            value: 'name',
          },
          {
            text: 'Описание',
            align: 'start',
            sortable: false,
            value: 'description',
          },
          {
            text: 'Домашняя страница',
            align: 'start',
            sortable: false,
            value: 'homepage',
          },
          {
            text: 'Github',
            align: 'start',
            sortable: false,
            value: 'github',
          },
        ],
      searchInProgress: false,
      actualNameForModal: '',
      errorText: '',
      tableItems: []
    }
  },
  methods: {
    openModalForPackage(packageInfo) {
      this.actualNameForModal = packageInfo.name
    },
    async search(value) {
      this.errorText = ''
      this.searchInProgress = true
      try {
        const result = await fetch(`https://api.jsdelivr.com/v1/jsdelivr/libraries?name=${value}`)
        if (result.status === 200) {
          const json = await result.json()
          this.tableItems = json
        } else {
          this.errorText = unknownError
        }
      } catch {
        this.errorText = unknownError
      } finally {
        this.searchInProgress = false
      }
    },
  },
  computed: {
    actualPackage() {
      return this.tableItems.find(item => item.name === this.actualNameForModal) || {}
    }
  },
}
</script>
