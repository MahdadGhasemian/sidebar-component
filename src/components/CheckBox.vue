<template>
  <div>
    <div class="container">
      <div class="header row py-1">
        <div
          v-for="(item, i) in items"
          :key="i"
          class="col-4 align-items-center"
        >
          <input
            class="form-check-input"
            type="checkbox"
            v-model="item.value"
          />
          <i :class="item.icon" style="color: white"></i>
        </div>
      </div>
      <div class="row">
        <template v-for="(item, i) in items" :key="i * 100">
          <template v-if="item.value">
            <div
              v-for="(child, j) in item.childs"
              :key="'child-' + j"
              class="col-12"
            >
              <div
                class="sub-item row p-2 align-items-center"
                :class="String(i) + String(j) === selected ? 'selected' : ''"
                @click="setSelect(i, j)"
              >
                <span class="col-4">{{ item.name }}</span>
                <i
                  class="col-4"
                  :class="item.icon"
                  :style="getColor(child.color)"
                ></i>
                <input class="col-4" v-model="child.value" type="number" />
              </div>
            </div>
          </template>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          id: 1,
          name: "box-corners",
          icon: "fa fa-sitemap",
          value: true,
          childs: [
            { value: 16, color: "yellow" },
            { value: 30, color: "green" },
            { value: 33, color: "pink" },
          ],
        },
        {
          id: 2,
          name: "person",
          icon: "fa fa-male",
          value: false,
        },
        {
          id: 3,
          name: "bounding box",
          icon: "fa fa-plus-circle",
          value: true,
          childs: [
            { value: 43, color: "green" },
            { value: 44, color: "yellow" },
          ],
        },
      ],
      selected: "",
    };
  },
  methods: {
    setSelect(i, j) {
      this.selected = String(i) + String(j);
    },
    getColor(color) {
      return "color: " + color;
    },
  },
};
</script>

<style scoped>
.container {
  max-width: 430px;
}

.test-border {
  border: solid 1px red;
}

.header {
  background-color: #102535;
  border-bottom: solid 1px gray;
}

.header i {
  color: white;
}

.sub-item {
  background-color: #102535;
  color: white;
}

.sub-item:hover {
  background-color: #607788;
  color: black;
}

.selected {
  opacity: 0.5;
}

.custom-checkbox .custom-control-input:checked ~ .custom-control-label::before {
  background-color: green !important;
}

.custom-checkbox
  .custom-control-input:checked:focus
  ~ .custom-control-label::before {
  box-shadow: 0 0 0 1px #fff, 0 0 0 0.2rem rgba(0, 255, 0, 0.25);
}
.custom-checkbox .custom-control-input:focus ~ .custom-control-label::before {
  box-shadow: 0 0 0 1px #fff, 0 0 0 0.2rem rgba(0, 0, 0, 0.25);
}
.custom-checkbox .custom-control-input:active ~ .custom-control-label::before {
  background-color: #c8ffc8;
}
</style>
