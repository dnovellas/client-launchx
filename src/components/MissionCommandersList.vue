<template>
  <div class="list row">
    <div class="col-md-6">
      <h4>MissionCommanders</h4>
      <ul class="list-group">
        <li
          class="list-group-item"
          :class="{ active: index == currentIndex }"
          v-for="(missionCommander, index) in missionCommanders"
          :key="index"
          @click="setActiveMissionCommander(missionCommander, index)"
        >
          {{ missionCommander.username }}
        </li>
      </ul>
    </div>
    <div class="col-md-6">
      <div v-if="currentMissionCommander">
        <h4>Mission Commanders</h4>
        <div>
          <div>
            <label><strong>Nombre:</strong></label>
            {{ currentMissionCommander.name }} <br />
          </div>
          <div>
            <label><strong>Username:</strong></label>
            {{ currentMissionCommander.username }} <br />
          </div>
          <div>
            <label><strong>Main Stack:</strong></label>
            {{ currentMissionCommander.mainStack }}<br />
          </div>
          <div>
            <label><strong>Current Enrollment:</strong></label>
            {{ currentMissionCommander.currentEnrollment }}<br />
          </div>
          <div>
            <label><strong>Has Azure Certification:</strong></label>
            {{ currentMissionCommander.hasAzureCertification }}
          </div>
        </div>
        <router-link
          :to="'/missionCommander/' + currentMissionCommander.id"
          class="btn btn-info"
        >
          Editar</router-link
        >
      </div>
      <div v-else>
        <br />
        <p>Selecciona un Mission Commander.</p>
      </div>
    </div>
  </div>
</template>
<script>
import MissionCommanderService from "../services/MissionCommanderService";

export default {
  name: "missionCommanders-list",
  data() {
    return {
      tutorials: [],
      missionCommanders: [],
      currentTutorial: null,
      currentMissionCommander: null,
      currentIndex: -1,
      title: "",
      missionCommanderId: "",
    };
  },
  methods: {
    getAllMissionCommanders() {
      MissionCommanderService.getAll()
        .then((response) => {
          this.missionCommanders = response.data;
        })
        .catch((e) => {
          console.log(e);
        });
    },
    setActiveMissionCommander(missionCommander, index) {
      this.currentMissionCommander = missionCommander;
      this.currentIndex = missionCommander ? index : -1;
    },
  },
  mounted() {
    this.getAllMissionCommanders();
  },
};
</script>
