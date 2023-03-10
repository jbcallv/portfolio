<template>
  <transition
    appear
    enter-active-class="animated fadeIn"
    leave-active-class="animated fadeOut"
  >
    <q-page class="flex flex-center">
      <div class="row full-width justify-center items-start">
        <div
          class="col-12 col-md-5 col-lg-4 col-xl-3 q-pr-xl q-pl-xl q-pt-xl q-pb-md"
        >
          <div class="text-h2 text-weight-light q-pb-lg gt-sm">Contact me</div>
          <div class="text-h3 text-center text-weight-light q-pb-lg lt-md">
            Contact me
          </div>

          <div class="text-h5 text-weight-light text-grey gt-sm q-pb-md">
            Want to get in touch? Either send me an email by filling out the
            form or connect with me through social media
          </div>

          <div
            class="text-h6 text-center text-weight-light text-grey lt-md q-pb-lg"
          >
            Want to get in touch? Either send me an email by filling out the
            form or connect with me through social media
          </div>

          <div
            class="text-h5 text-weight-light text-grey gt-sm q-pb-lg q-gutter-md"
          >
            <q-btn
              class="q-pa-none"
              icon="fa-brands fa-linkedin"
              unelevated
              @click="openURL(linkedinUrl)"
            />
            <q-btn
              class="q-pa-none"
              icon="fa-brands fa-github"
              unelevated
              @click="openURL(githubUrl)"
            />
          </div>

          <div
            class="text-h5 text-center text-weight-light text-grey q-pb-lg lt-md q-gutter-md"
          >
            <q-btn
              class="q-pa-none"
              icon="fa-brands fa-linkedin"
              unelevated
              @click="openURL(linkedinUrl)"
            />
            <q-btn
              class="q-pa-none"
              icon="fa-brands fa-github"
              @click="openURL(githubUrl)"
            />
          </div>
        </div>

        <q-form
          @submit="sendEmail()"
          class="col-10 col-md-5 col-lg-4 col-xl-3 q-gutter-y-sm"
        >
          <div class="row q-gutter-lg justify-center">
            <div class="col">
              <q-input
                filled
                v-model="firstName"
                label="First name"
                dark
                color="secondary"
                lazy-rules
                :rules="[
                  (val) =>
                    (!!val && val.length > 0) || 'Please enter your first name',
                ]"
              />
            </div>
            <div class="col">
              <q-input
                filled
                v-model="lastName"
                label="Last name"
                dark
                color="secondary"
                lazy-rules
                :rules="[
                  (val) =>
                    (!!val && val.length > 0) || 'Please enter your last name',
                ]"
              />
            </div>
          </div>

          <div class="row justify-center">
            <div class="col-12">
              <q-input
                filled
                v-model="emailAddress"
                label="Email"
                dark
                color="secondary"
                lazy-rules
                :rules="[
                  (val) =>
                    (!!val && val.length > 0) || 'Please enter your email',
                ]"
              />
            </div>
          </div>

          <div class="row justify-center q-pb-sm">
            <div class="col-12">
              <q-input
                filled
                v-model="details"
                label="Let's talk about..."
                dark
                type="textarea"
                color="secondary"
                lazy-rules
                :rules="[
                  (val) =>
                    (!!val && val.length > 0) ||
                    'Please enter something you wish to talk about',
                ]"
              />
            </div>
          </div>

          <div class="row justify-center">
            <div class="col-4 col-md-3">
              <q-btn
                no-caps
                rounded
                size="18px"
                class="text-weight-regular full-width"
                label="Submit"
                color="primary"
                type="submit"
              />
            </div>
          </div>
        </q-form>
      </div>
    </q-page>
  </transition>
</template>

<script>
import { openURL, useQuasar } from "quasar";
import { ref } from "vue";
import emailjs from "@emailjs/browser";

export default {
  name: "ContactPage",

  setup() {
    const $q = useQuasar();

    const firstName = ref("");
    const lastName = ref("");
    const emailAddress = ref("");
    const details = ref("");

    function sendEmail() {
      const emailTemplateParameters = createTemplateParameters();

      emailjs
        .send(
          import.meta.env.VITE_EMAILJS_SERVICE_ID,
          import.meta.env.VITE_EMAILJS_TEMPLATE_ID,
          emailTemplateParameters,
          import.meta.env.VITE_EMAILJS_PUBLIC_KEY
        )
        .then(() => {
          makeSuccessNotification(
            "Your message has been sent. I will get back to you as soon as possible"
          );
        })
        .catch((error) => {
          console.log(error);
          makeErrorNotification(
            "Failed to send message. Email me directly at jbcallv@gmail.com"
          );
        });
    }

    function createTemplateParameters() {
      return {
        from_name: `${firstName.value} ${lastName.value}`,
        reply_to: emailAddress.value,
        message: details.value,
      };
    }

    function makeSuccessNotification(message) {
      $q.notify({
        type: "positive",
        message: message,
      });
    }

    function makeErrorNotification(message) {
      $q.notify({
        type: "negative",
        message: message,
      });
    }

    return {
      openURL,
      linkedinUrl: "https://www.linkedin.com/in/jbcallv",
      githubUrl: "https://github.com/jbcallv",

      firstName,
      lastName,
      emailAddress,
      details,

      sendEmail,
    };
  },
};
</script>
