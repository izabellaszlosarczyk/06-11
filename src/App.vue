<template>
  <div class="container-fluid">
    <nav class="navbar navbar-dark bg-dark">
      <span class="navbar-brand mb-0 h1">Participants list</span>
    </nav>
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
  export default {
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