<template>
  <section
    v-if="showCookieConsent"
    class="fixed max-w-md p-4 mx-auto bg-white border border-gray-200 dark:bg-gray-800 left-4 bottom-4 md:left-12 md:bottom-16 dark:border-gray-700 rounded-2xl"
  >
    <h2 class="title text-gray-800 dark:text-white">🍪 We use cookies!</h2>
    <p class="paragraph-info mt-4 text-sm text-gray-600 dark:text-gray-300">
      Hi, this website uses essential cookies to ensure its proper operation and
      tracking cookies to understand how you interact with it. The latter will
      be set only after consent.
    </p>

    <p
      class="second-paragraph-info mt-3 text-sm text-gray-600 dark:text-gray-300"
    >
      Closing this modal default settings will be saved.
    </p>
    <div class="grid grid-cols-2 gap-4 mt-4">
      <button
        @click="acceptCookies"
        class="buttons w-auto text-xs bg-gray-900 font-medium rounded-lg hover:bg-gray-700 text-white px-4 py-2.5 duration-300 transition-colors focus:outline-none"
      >
        Accept all
      </button>
      <button
        @click="rejectCookies"
        class="buttons w-auto text-xs border text-gray-800 hover:bg-gray-100 dark:border-gray-700 dark:text-white dark:hover:bg-gray-700 font-medium rounded-lg px-4 py-2.5 duration-300 transition-colors focus:outline-none"
      >
        Reject all
      </button>
      <button
        @click="closeModal"
        class="buttons w-auto text-xs border text-gray-800 hover:bg-gray-100 dark:border-gray-700 dark:text-white dark:hover:bg-gray-700 font-medium rounded-lg px-4 py-2.5 duration-300 transition-colors focus:outline-none col-span-2"
      >
        Close
      </button>
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  data(): { showCookieConsent: boolean } {
    return {
      showCookieConsent: true,
    };
  },
  methods: {
    acceptCookies(): void {
      console.log("Cookies accepted");
      sessionStorage.setItem("cookieConsent", "accepted");
      this.closeModal();
    },
    rejectCookies(): void {
      console.log("Cookies rejected");
      sessionStorage.setItem("cookieConsent", "rejected");
      this.closeModal();
    },
    closeModal(): void {
      // Logic to close the cookie consent modal
      console.log("Modal closed");
      this.showCookieConsent = false;
    },
    checkCookieConsent(): void {
      const consent = sessionStorage.getItem("cookieConsent");
      // If the user has already accepted or rejected cookies, do not show the consent modal
      if (consent === "accepted" || consent === "rejected") {
        this.showCookieConsent = false;
      }
    },
  },
  mounted(): void {
    // When the component is mounted, check if the user has already made a cookie consent decision
    this.checkCookieConsent();
  },
});
</script>

<style scoped>
.title {
  font-family: "Open Sans", Arial, Helvetica, sans-serif;
  font-weight: 400;
}

.paragraph-info {
  font-family: "Open Sans", Arial, Helvetica, sans-serif;
  font-weight: 400;
}

.second-paragraph-info {
  font-family: "Open Sans", Arial, Helvetica, sans-serif;
  font-weight: 400;
}

.buttons {
  font-family: "Open Sans", Arial, Helvetica, sans-serif !important;
  font-size: 14px;
  font-weight: 700;
}
</style>
