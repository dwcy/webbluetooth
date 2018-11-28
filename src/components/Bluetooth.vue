<template>
  <div>
  <button v-on:click="scanBlueToothDevice">SCAN</button>
  <br>
  bluetooth:{{bluetooth}}
  <br>
  {{connectedDevice}}
  <br>
  {{service}}
  <br>
  {{value}}
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      bluetooth: "",
      connectedDevice: "",
      service: "",
      value: ""
    }
  },
  methods: {
    scanBlueToothDevice() {
       this.bluetooth =('Requesting Bluetooth Device...');
        navigator.bluetooth.requestDevice(
          {filters: [{services: ['battery_service']}]})
        .then(device => {
          this.bluetooth =('Connecting to GATT Server...');
          this.connectedDevice = device.gatt.connect();
        })
        .then(server => {
          this.bluetooth =('Getting Battery Service...');
          this.service = server.getPrimaryService('battery_service');
        })
        .then(service => {
          this.bluetooth =('Getting Battery Level Characteristic...');
          this.service = service.getCharacteristic('battery_level');
        })
        .then(characteristic => {
          this.bluetooth = ('Reading Battery Level...');
          this.value = characteristic.readValue();
        })
        .then(value => {
          let batteryLevel = value.getUint8(0);
          this.bluetooth =( '> Battery Level is ' + batteryLevel + '%');
        })
        .catch(error => {
          this.bluetooth = ('Argh! ' + error);
        });
    }
  }
};
</script>

<style scoped lang="scss">

button {
  color: white;
  font-weight: bold;
  background: #444;
  border: 2px solid #444;
  width: 84px;
  padding-top: 10px;
  padding-bottom: 10px;
  cursor: pointer;
}
</style>
