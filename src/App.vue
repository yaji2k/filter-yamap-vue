F<template>
  <div id="app" class="wrapper">
    <yandex-map
      :coords="[54.62896654088406, 39.731893822753904]"
      zoom="10"
      class="map"
      :cluster-options="{
        1: {clusterDisableClickZoom: true}
      }"
      :controls="[]"
      :placemarks="placemarks"
      map-type="map"
      :zoom-control="{
        options: {
            size: 'small'
        }
      }"
    ></yandex-map>
    <div class="map_btn">
      <button :class="['btn', {active: allStatus}]" @click="changeStatusAll()">all</button>
      <buttons-app :list="list" class="center" @change-status="changeStatus($event)"></buttons-app>
    </div>
  </div>
</template>

<script>
import ButtonsApp from "./components/Buttons";
import { yandexMap } from "vue-yandex-maps";

export default {
  name: "app",
  components: {
    ButtonsApp,
    yandexMap
  },
  data() {
    return {
      list: [],
      placemarksList: {
        cafes: [
          {
            coords: [54.8, 39.8],
            properties: {}, // define properties here
            options: {}, // define options here
            clusterName: "1",
            balloonTemplate: '<div>"Your custom template"</div>'
          },
          {
            coords: [54.8, 39.7],
            properties: {}, // define properties here
            options: {}, // define options here
            clusterName: "1",
            balloonTemplate: '<div>"Your custom template"</div>'
          }
        ],
        banks: [
          {
            coords: [54.7, 39.8],
            properties: {}, // define properties here
            options: {
              preset: "islands#dotIcon",
              iconColor: "green"
            }, // define options here
            clusterName: "1",
            balloonTemplate: '<div>"Your custom template"</div>'
          },
          {
            coords: [54.6, 39.6],
            properties: {}, // define properties here
            options: {
              preset: "islands#dotIcon",
              iconColor: "green"
            }, // define options here
            clusterName: "1",
            balloonTemplate: '<div>"Your custom template"</div>'
          }
        ],
        parks: [
          {
            coords: [54.7, 39.9],
            properties: {
              hintContent: "что это?"
            }, // define properties here
            options: {
              preset: "islands#dotIcon",
              iconColor: "red"
            }, // define options here
            clusterName: "1",
            balloonTemplate: '<div>"Your custom template"</div>'
          },
          {
            coords: [54.6, 39.9],
            properties: {}, // define properties here
            options: {
              preset: "islands#dotIcon",
              iconColor: "red"
            }, // define options here
            clusterName: "1",
            balloonTemplate: '<div>"Your custom template"</div>'
          }
        ]
      }
    };
  },
  beforeMount() {
    for (let index in this.placemarksList) {
      this.list.push({
        name: index,
        status: true
      });
    }
  },
  methods: {
    changeStatus(event) {
      this.list[event.key].status = !this.list[event.key].status;
    },
    changeStatusAll() {
      let status = !this.allStatus;
      for (let value of this.list) {
        value.status = status;
      }
    }
  },
  computed: {
    listItems() {
      return this.list.filter(({ status }) => status).map(el => el.name);
    },
    placemarks() {
      let marks = [];
      this.listItems.forEach(index => {
        marks = [...marks, ...this.placemarksList[index]];
      });
      return marks;
    },
    allStatus() {
      let count = 0;
      this.list.forEach(el => {
        if (el.status) {
          count++;
        }
      });
      return this.list.length === count ? true : false;
    }
  }
};
</script>
<style scope>
.wrapper {
  position: relative;
  max-width: 1024px;
  margin: 0px auto;
}
.center {
  display: flex;
  justify-content: center;
}
.map {
  width: 100%;
  height: 100vh;
}
.map_btn {
  position: absolute;
  top: 0;
  left: 1%;
  margin-top: 5px;
  display: flex;
}
.btn {
  margin-left: 5px;
  margin-right: 5px;
  font-size: 1.1em;
  border-radius: 5px;
  border-color: transparent;
  box-shadow: 0 1px 2px 1px rgba(0, 0, 0, 0.15),
    0 2px 5px -3px rgba(0, 0, 0, 0.15);
  color: rgba(0, 0, 0, 0.5);
  background: rgba(0, 0, 0, 0.25);

  cursor: pointer;
  outline: none;
}
.active {
  color: black;
  background: white;
}
</style>

