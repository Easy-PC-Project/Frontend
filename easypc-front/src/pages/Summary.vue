<template>
  <div>
    <p class="Summary pt-4">Resumen # {{ CurrentBuild.idBuild }}</p>
    <p class="user">Build para {{ user }}</p>
    <div class="pt-2 parts row accordion">
      <div
        class="p-1 col-12 col-md-8 col-lg-6 offset-lg-0 offset-md-2 offset-sm-0"
        v-if="CurrentCPU"
      >
        <ComponentView v-bind:Parte="CurrentCPU" tipo="CPU" class="screen" />
      </div>

      <div
        class="p-1 col-12 col-md-8 col-lg-6 offset-lg-0 offset-md-2 offset-sm-0"
        v-if="CurrentGPU"
      >
        <ComponentView v-bind:Parte="CurrentGPU" tipo="GPU" class="screen" />
      </div>
      <div
        class="p-1 col-12 col-md-8 col-lg-6 offset-lg-0 offset-md-2 offset-sm-0"
        v-if="CurrentMotherboard"
      >
        <ComponentView
          v-bind:Parte="CurrentMotherboard"
          tipo="Motherboard"
          class="screen"
        />
      </div>
      <div
        class="p-1 col-12 col-md-8 col-lg-6 offset-lg-0 offset-md-2 offset-sm-0"
        v-if="CurrentRAM"
      >
        <ComponentView v-bind:Parte="CurrentRAM" tipo="RAM" class="screen" />
      </div>
      <div
        class="p-1 col-12 col-md-8 col-lg-6 offset-lg-0 offset-md-2 offset-sm-0"
        v-if="CurrentCooling"
      >
        <ComponentView
          v-bind:Parte="CurrentCooling"
          tipo="Cooling"
          class="screen"
        />
      </div>
      <div
        class="p-1 col-12 col-md-8 col-lg-6 offset-lg-0 offset-md-2 offset-sm-0"
        v-if="CurrentSSD"
      >
        <ComponentView v-bind:Parte="CurrentSSD" tipo="SSD" class="screen" />
      </div>
      <div
        class="p-1 col-12 col-md-8 col-lg-6 offset-lg-0 offset-md-2 offset-sm-0"
        v-if="CurrentHDD"
      >
        <ComponentView v-bind:Parte="CurrentHDD" tipo="HDD" class="screen" />
      </div>
      <div
        class="p-1 col-12 col-md-8 col-lg-6 offset-lg-0 offset-md-2 offset-sm-0"
        v-if="CurrentPowerSupply"
      >
        <ComponentView
          v-bind:Parte="CurrentPowerSupply"
          tipo="PowerSupply"
          class="screen"
        />
      </div>
      <div
        class="p-1 col-12 col-md-8 col-lg-6 offset-lg-0 offset-md-2 offset-sm-0"
        v-if="CurrentMouse"
      >
        <ComponentView
          v-bind:Parte="CurrentMouse"
          tipo="Mouse"
          class="screen"
        />
      </div>
      <div
        class="p-1 col-12 col-md-8 col-lg-6 offset-lg-0 col-lg-6 offset-lg-0 offset-md-2 offset-sm-0"
        v-if="CurrentKeyboard"
      >
        <ComponentView
          v-bind:Parte="CurrentKeyboard"
          tipo="Keyboard"
          class="screen"
        />
      </div>
      <div
        class="p-1 col-12 col-md-8 col-lg-6 offset-lg-0 offset-md-2 offset-sm-0"
        v-if="CurrentMonitor"
      >
        <ComponentView
          v-bind:Parte="CurrentMonitor"
          tipo="Monitor"
          class="screen"
        />
      </div>
      <div
        class="p-1 col-12 col-md-8 col-lg-6 offset-lg-0 offset-md-2 offset-sm-0"
        v-if="CurrentCase"
      >
        <ComponentView v-bind:Parte="CurrentCase" tipo="Case" class="screen" />
      </div>
      <div>
        <ComponentViewPrint
          v-bind:Parte="CurrentCPU"
          tipo="CPU"
          class="print"
        />
        <ComponentViewPrint
          v-bind:Parte="CurrentGPU"
          tipo="GPU"
          class="print"
        />
        <ComponentViewPrint
          v-bind:Parte="CurrentMotherboard"
          tipo="Motherboard"
          class="print"
        />
        <ComponentViewPrint
          v-bind:Parte="CurrentRAM"
          tipo="RAM"
          class="print"
        />
        <ComponentViewPrint
          v-bind:Parte="CurrentCooling"
          tipo="Cooling"
          class="print"
        />
        <ComponentViewPrint
          v-bind:Parte="CurrentSSD"
          v-if="CurrentSSD"
          tipo="SSD"
          class="print"
        />
        <ComponentViewPrint
          v-bind:Parte="CurrentHDD"
          v-if="CurrentHDD"
          tipo="HDD"
          class="print"
        />
        <ComponentViewPrint
          v-bind:Parte="CurrentPowerSupply"
          tipo="PowerSupply"
          class="print"
        />
        <ComponentViewPrint
          v-bind:Parte="CurrentMouse"
          v-if="CurrentMouse"
          tipo="Mouse"
          class="print"
        />
        <ComponentViewPrint
          v-bind:Parte="CurrentKeyboard"
          v-if="CurrentKeyboard"
          tipo="Keyboard"
          class="print"
        />
        <ComponentViewPrint
          v-bind:Parte="CurrentMonitor"
          v-if="CurrentMonitor"
          tipo="Monitor"
          class="print"
        />
        <ComponentViewPrint
          v-bind:Parte="CurrentCase"
          tipo="Case"
          class="print"
        />
      </div>
      <div class="container">
        <h2 class="TotalPrice">
          Total Minimo: ${{
            Total.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")
          }}
          COP
        </h2>
      </div>
      <div class="col-12 col-sm-6 col-md-5 offset-md-6 mb-3">
        <vs-button
          class="screen"
          block
          @click="saveModel"
          color="rgb(59,22,100)"
        >
          <h2>Guardar Build</h2>
        </vs-button>
        <div>
          <vs-button class="screen" @click="printDiv" color="rgb(59,22,100)">
            <h2>Guardar como PDF</h2>
          </vs-button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ComponentView from "../components/Summary/ComponentView";
import ComponentViewPrint from "../components/Summary/ComponentViewPrint";
import EasyPCService from "../services/EasyPCService";

export default {
  name: "Summary",
  components: {
    ComponentView,
    ComponentViewPrint,
  },
  data() {
    return {
      CurrentBuild: [],
      CurrentCPU: [],
      CurrentGPU: [],
      CurrentMotherboard: [],
      CurrentRAM: [],
      CurrentCooling: [],
      CurrentSSD: [],
      CurrentHDD: [],
      CurrentPowerSupply: [],
      CurrentMouse: [],
      CurrentKeyboard: [],
      CurrentMonitor: [],
      CurrentCase: [],
      user: this.$store.getters.getUser,
      Total: Number,
      retrievedBuildID: Number,
    };
  },
  props: {
    id: Number,
  },
  methods: {
    retrieveBuildFromDB(id) {
      EasyPCService.getBuildById(id)
        .then((response) => {
          this.CurrentBuild = response.data;
          this.CurrentCPU = this.CurrentBuild.cpu;
          this.CurrentGPU = this.CurrentBuild.gpu;
          this.CurrentMotherboard = this.CurrentBuild.motherboard;
          this.CurrentRAM = this.CurrentBuild.ram;
          this.CurrentCooling = this.CurrentBuild.cooling;
          this.CurrentSSD = this.CurrentBuild.ssd;
          this.CurrentHDD = this.CurrentBuild.hdd;
          this.CurrentPowerSupply = this.CurrentBuild.powerSupply;
          this.CurrentMouse = this.CurrentBuild.mouse;
          this.CurrentKeyboard = this.CurrentBuild.keyboard;
          this.CurrentMonitor = this.CurrentBuild.monitor;
          this.CurrentCase = this.CurrentBuild.caseObj;
        })
        .catch((e) => {
          console.log(e);
        });
      EasyPCService.getBuildPriceById(id)
        .then((response) => {
          this.Total = response.data;
        })
        .catch((e) => {
          console.log(e);
        });
    },
    retrieveBuildFromAnswers(answers) {
      EasyPCService.getRecommendedBuild(answers)
        .then((response) => {
          this.CurrentBuild = response.data;
          this.CurrentCPU = this.CurrentBuild.cpu;
          this.CurrentGPU = this.CurrentBuild.gpu;
          this.CurrentMotherboard = this.CurrentBuild.motherboard;
          this.CurrentRAM = this.CurrentBuild.ram;
          this.CurrentCooling = this.CurrentBuild.cooling;
          this.CurrentSSD = this.CurrentBuild.ssd;
          this.CurrentHDD = this.CurrentBuild.hdd;
          this.CurrentPowerSupply = this.CurrentBuild.powerSupply;
          this.CurrentMouse = this.CurrentBuild.mouse;
          this.CurrentKeyboard = this.CurrentBuild.keyboard;
          this.CurrentMonitor = this.CurrentBuild.monitor;
          this.CurrentCase = this.CurrentBuild.caseObj;
        })
        .catch((e) => {
          console.log(e);
        });

      EasyPCService.getRecommendedPrice(answers)
        .then((response) => {
          this.Total = response.data;
        })
        .catch((e) => {
          console.log("Retrive price error: " + e);
        });
    },
    saveModel() {
      if (!this.$store.getters.getAuthenticated) {
        this.$router.push({ name: "Login" });
      } else {
        var data = {
          idBuild: null,
          cpu: this.CurrentBuild.cpu,
          gpu: this.CurrentBuild.gpu,
          motherboard: this.CurrentBuild.motherboard,
          ram: this.CurrentBuild.ram,
          cooling: this.CurrentBuild.cooling,
          ssd: this.CurrentBuild.ssd,
          hdd: this.CurrentBuild.hdd,
          powerSupply: this.CurrentBuild.powerSupply,
          mouse: this.CurrentBuild.mouse,
          keyboard: this.CurrentBuild.keyboard,
          monitor: this.CurrentBuild.monitor,
          caseObj: this.CurrentBuild.caseObj,
          user: {
            username: this.user,
          },
        };
        EasyPCService.createBuild(data)

          .then(() => {
            this.$router.push({ name: "MyBuilds" });
          })
          .catch((e) => {
            console.log(e);
          });
      }
    },
    printDiv() {
      document.title = "Easy PC Build";
      window.print();
    },
  },
  mounted() {},
  beforeMount() {
    if (this.$store.getters["getInterIDBuild"] != -1) {
      this.retrieveBuildFromDB(this.$store.getters["getInterIDBuild"]);
      this.retrievedBuildID = this.$store.getters["getInterIDBuild"];
      this.$store.commit("setInterIDBuild", -1);
    } else {
      this.retrieveBuildFromAnswers(this.$store.getters["getAnswers"]);
      this.$store.commit("emptyAnswers");
    }
  },
};
</script>



<style scoped >
@import url(https://fonts.googleapis.com/css2?family=Fredoka+One&display=swa);
@import url(https://fonts.googleapis.com/css2?family=Maven+Pro:wght@700&display=swap);

.TotalPrice {
  font-size: calc(1.8rem + 1.7vw);
  font-family: "Fredoka One", cursive;
  color: #ff9941;
  background-color: rgb(24, 23, 23);
}

.Summary {
  font-family: "Maven Pro", sans-serif;
  font-size: calc(1.9rem + 3.8vw);
  color: rgb(24, 23, 23);
}

.parts {
  animation: animacion;
  animation-duration: 2s;
}

.user {
  font-size: calc(1rem + 1.5vw);
  font-family: "Maven Pro", sans-serif;
  color: rgb(24, 23, 23);
}

.print {
  display: none;
}

@media print {
  .screen {
    display: none;
  }
  .print {
    display: block;
  }
}

@keyframes animacion {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}
</style>