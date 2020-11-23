<template>
    <div class="participants-list">
      <h1>Participants</h1>
      <div v-if="participants.length > 0">
        <div v-for="participant in participants" v-bind:key="participant.id">
          {{participant.name}} {{participant.surname}}
          <button v-on:click="onRemove(participant)" type="button" class="btn btn-danger">Remove</button>
        </div>
      </div>
      <div v-else class="alert alert-info" role="alert">
        Oopsss. Nothing here ;c 
      </div>
    </div>
</template>

<script>
export default {
    props: ['participants'],
    data: function (){ return {}},
    methods: {
        onRemove: function (participant){
            this.$emit('participant-remove', participant);
        }
    }
}
</script>

<style>

</style>