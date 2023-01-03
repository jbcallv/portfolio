<template>
  <q-page class="flex flex-center">
    <div class="row full-width justify-center items-center">
      <div class="col-12 justify-center lt-md q-pb-xl">
        <div class="row justify-center full-height">
          <div
            class="col-12 bg-dark"
            style="position: absolute; height: 590px; width: 400px"
          ></div>
          <q-img
            src="images/joseph.jpg"
            class="q-mt-lg"
            style="height: 590px; width: 330px"
          />
        </div>
      </div>

      <div class="col-12 col-md-5 col-lg-4 col-xl-3 text-left">
        <div class="text-h2 text-weight-light q-pb-lg gt-sm">
          Hi, I'm Joseph.
        </div>
        <div class="text-h3 text-weight-light q-pb-lg lt-md">
          Hi, I'm Joseph.
        </div>

        <div class="text-h5 text-weight-light text-grey">
          Full Stack Developer from Virginia, USA. I create web applications
          with modern frameworks. Welcome to my corner of the internet!
        </div>
      </div>

      <div class="col-12 col-md-5 col-lg-4 col-xl-3 text-center gt-sm">
        <div class="row justify-center full-height">
          <div
            class="col-6 bg-dark"
            style="position: absolute; height: 590px; width: 400px"
          ></div>
          <q-img
            src="images/joseph.jpg"
            class="q-mt-lg"
            style="height: 590px; width: 350px"
          />
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
});
</script>
