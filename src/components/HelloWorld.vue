<template>
  <div>
    <div
      ref="configurator"
      style="width:800px;height:600px;"
    >

    </div>
  </div>
</template>

<script lang="ts">
  import RoomleSdk from "@roomle/web-sdk";

  import {
    onMounted,
    ref,
  } from 'vue';

  export default {
    setup() {
      const configurator = ref(null);

      onMounted(async () => {
        const roomleConfigurator = await RoomleSdk.getConfigurator();
        roomleConfigurator.boot();
        RoomleSdk.setGlobalInitData({customApiUrl: 'https://api.roomle.com/v2'});
        await roomleConfigurator.getApi().init(configurator.value);
        await roomleConfigurator.getApi().loadConfigurableItemById("usm:frame");
      });

      return {
        configurator,
      };
    },
  };
</script>
