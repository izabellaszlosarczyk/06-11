<template>
  <div class="container-fluid">
    <nav class="navbar navbar-dark bg-dark">
      <span class="navbar-brand mb-0 h1">Participants list</span>
    </nav>
    <participants-list v-bind:participants="participants" v-on:participant-remove="onRemove($event)"></participants-list>
    <div class="participant-add-form">
      <h1>Add participant</h1>
      <form v-on:submit.prevent="onSubmit()">
        <div class="form-group">
          <label for="formName">Name</label>
          <input v-model="newParticipantName" type="text" class="form-control" id="formName" placeholder="Participant name">
        </div>
        <div class="form-group">
          <label for="formSurname">Surname</label>
          <input v-model="newParticipantSurname" type="text" class="form-control" id="formSurname" placeholder="Participant surname">
        </div>
        <button type="submit" class="btn btn-info">Submit</button>
      </form>
    </div>
  </div>
</template>

<script>
  import ParticipantsList from "./components/ParticipantsList.vue";

  export default {
    components: {ParticipantsList},
    data: function () {
      return {
        participants: [],
        newParticipantName: null,
        newParticipantSurname: null,
      }
    },
    methods: {
      onSubmit: function (){
        var newParticipant = {
          name: this.newParticipantName,
          surname: this.newParticipantSurname,
          id: Math.random() * 1000,
        };
        this.participants.push(newParticipant);
        this.newParticipantName = null;
        this.newParticipantSurname = null;
      },
      onRemove: function (participant){
        this.participants = this.participants.filter((p) => { return p.id !== participant.id});
      }
    }
  };
</script>

<style>
  .container-fluid {
    padding: 0;
    margin: 0;
  }

  .participant-add-form {
    margin: 20px;
  }

  .participant-add-form h1 {
    background-color: #BFBFBD;
    border-left: 2px solid #444;
    padding: 15px;
    color: white;
  }

  .participants-list {
    margin: 20px;
  }
</style>