<template>
  <div>
    <div v-if="has_linked_station">
      <h3>Linked Station Info</h3>
      <span :class="station_locked_in ? 'good' : 'bad'">{{ station_locked_in ? 'Locked In ' : 'Not Locked In ' }}</span><span :class="station_locked_in ? 'good' : 'bad'">({{ locked_in_name }})</span>
      <br><span>Calibration: {{calibration}}%</span> <vui-button :params="{ recalibrate: 1 }">Recalibrate</vui-button>
      <h3>Teleporter Beacons</h3>
      <table class="table border">
        <tr class="header border">
          <th>Beacon Name</th>
          <th>Action</th>
        </tr>
        <tr v-for="beacon in teleport_beacons" class="item border" :key="beacon.ref">
          <td>{{ beacon.beacon_name }}</td>
          <td>
            <vui-button :class="{ 'danger' : beacon.selected_beacon == true}" :params="{ beacon: beacon.ref, name: beacon.beacon_name }">{{beacon.selected_beacon == true ? "Unset" : "Lock On"}}</vui-button>
          </td>
        </tr>
      </table>
      <h3>Tracking Implants</h3>
      <table class="table border">
        <tr class="header border">
          <th>Implant Name</th>
          <th>Action</th>
        </tr>
        <tr v-for="implant in teleport_implants" class="item border" :key="implant.ref">
          <td>{{ implant.implant_name }}</td>
          <td>
            <vui-button :class="{ 'danger' : implant.selected_implant == true}" :params="{ implant: implant.ref, name: implant.implant_name }">{{implant.selected_implant == true ? "Unset" : "Lock On"}}</vui-button>
          </td>
        </tr>
      </table>
    </div>
    <div v-else>
      <h3>Nearby Teleportation Stations</h3>
      <table class="table border">
        <tr class="header border">
          <th>Name</th>
          <th>Action</th>
        </tr>
        <tr v-for="station in nearby_stations" class="item border" :key="station.ref">
          <td>{{ station.station_name }}</td>
          <td>
            <vui-button :params="{ station: station.ref }">Link</vui-button>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return this.$root.$data.state;
  }
};
</script>

<style lang="scss" scoped>
table {
  width: 100%;
  text-align: center;
}
tr {
  line-height: 135%;
}
</style>