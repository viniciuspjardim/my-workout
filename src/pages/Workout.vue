<template>
  <q-page class="bg-grey-3 column">
    <div
      class="absolute-bottom-right q-pa-lg">
      <q-btn
        @click="addDialogOpen = true"
        round
        color="secondary"
        icon="add" />
    </div>

    <q-list
      class="bg-white"
      separator>
      <exercise
        v-for="exercise in exercises"
        :key="exercise.id"
        :exercise="exercise"
      ></exercise>
    </q-list>

    <q-dialog v-model="addDialogOpen">
      <add-exercise @onAddSubmit='addDialogOpen = false'></add-exercise>
    </q-dialog>

  </q-page>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'

export default {
  data() {
    return {
      addDialogOpen: false
    }
  },
  computed: {
    ...mapGetters('workouts', ['exercises'])
  },
  methods: {
    ...mapActions('workouts', ['fetchExercises'])
  },
  components: {
    'exercise' : require('components/Workouts/Exercise.vue').default,
    'add-exercise' : require('components/Workouts/Modals/AddExercise.vue').default
  },
  created() {
    this.fetchExercises()
  }
}
</script>

<style lang="sass">
.done
  .q-item__label
    text-decoration: line-through
    color: #bbb
</style>
