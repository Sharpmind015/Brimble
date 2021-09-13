<script>
import { ref } from "vue";
import { gsap } from "gsap";
import Heading from "../components/Heading.vue";
import {
  Dialog,
  DialogOverlay,
  DialogTitle,
  DialogDescription,
} from "@headlessui/vue";

export default {
  name: "Hero",
  components: {
    Heading,
    Dialog,
    DialogOverlay,
    DialogTitle,
    DialogDescription,
  },
  data() {
    return {
      tools: [
        {
          name: "vue",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631510746/vue_ml7atz.svg",
        },
        {
          name: "ember",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631510817/ember_xjetmd.svg",
        },
        {
          name: "react",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631510883/react_knhn9b.svg",
        },
        {
          name: "nuxt",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631510913/nuxt_egzrba.svg",
        },
        {
          name: "gatsby",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631510941/gatsby_xkzjth.svg",
        },
        {
          name: "svelte",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631510975/svelte_xwiupt.svg",
        },
        {
          name: "angular",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631511025/angular_lkh7fl.svg",
        },
        {
          name: "next",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631511058/next_vjvp3a.svg",
        },
        {
          name: "javascript",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631511086/javascript_djuubq.svg",
        },
      ],
      showModal: false,
      response: {
        status: "",
        data: {
          number: "",
        },
      },
    };
  },
  mounted() {
    const headingTl = gsap.timeline({ repeat: -1, yoyo: true });
    headingTl
      .from(".heading-gradient", { opacity: 0, duration: 1.6 })
      .from(".heading-color", { opacity: 1, duration: 1.6 }, "-=1.6");
    const dotsTl = gsap.timeline({ repeat: -1, yoyo: true });
    dotsTl
      .fromTo(
        `.dots-up circle`,
        { scale: 0 },
        { scale: 1, stagger: 0.005, duration: 1.2, ease: "Bounce.in" }
      )
      .fromTo(
        `.dots-down circle`,
        { scale: 0 },
        { scale: 1, stagger: 0.005, duration: 1.2, ease: "Bounce.in" }
      );
    function onCompleteAnim() {
      gsap.to(`.nuxt`, { left: "25.5%", delay: 0.2 });
      gsap.to(`.svelte`, { right: "25.5%", delay: 0.2 });
      headingTl.pause();
      dotsTl.pause();
      gsap.set(".heading-gradient", { opacity: 1 });
      gsap.set(".heading-color", { opacity: 0 });
      gsap.set(".dots-up circle, .dots-down circle", { scale: 1 });
    }
    gsap.fromTo(
      `.tool-anim`,
      { opacity: 0 },
      {
        opacity: 1,
        stagger: 1.2,
        ease: "Bounce.out",
        onComplete: function () {
          onCompleteAnim();
        },
      }
    );
  },
  setup() {
    let isOpen = ref(false);

    return {
      isOpen,
      setIsOpen(value) {
        isOpen.value = value;
      },
    };
  },
  props: ["isToggle"],
  methods: {
    handleSubmit() {
      //API test :)
      this.response = {
        status: "Yay, we did it!!",
        data: {
          number: 666,
        },
      };
      //response ? 'Show animation' : 'return or error modal, whatever floats your boat :)'
      if (!this.isOpen) {
        this.setIsOpen(true);
      }
    },
    closeModal() {
      this.setIsOpen(true);
    },
  },
};
</script>

<template>
  <section class="hero">
    <div class="tools">
      <img
        :class="`absolute ${tool.name} hidden md:block tool tool-anim`"
        :src="tool.src"
        alt=""
        :key="index"
        v-for="(tool, index) in tools"
      />
    </div>
    <Heading :toggle="isToggle" />
    <p class="info">Be the first to know when BRIMBLE launches</p>
    <form @submit.prevent="handleSubmit" class="form">
      <label class="visuallyHidden" for="waitlist">
        Input your email address
      </label>
      <input
        required
        placeholder="email address"
        class="input-mail"
        type="email"
        name="waitlist"
        id="waitlist"
      />
      <input class="form-btn" type="submit" value="Join Waitlist" />
    </form>
    <Dialog class="modal" :open="isOpen" @close="setIsOpen">
      <DialogOverlay class="overlay" />

      <DialogTitle class="visuallyHidden">Status message</DialogTitle>
      <DialogDescription class="visuallyHidden">
        {{ response.status }}
      </DialogDescription>

      <div class="modal-tick">
        <svg
          width="60"
          height="38"
          viewBox="0 0 60 38"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <rect
            class="h-0 rect-1"
            width="4.83068"
            rx="2.41534"
            transform="matrix(-0.855371 0.518015 -0.495837 -0.868415 16.1709 35.8726)"
            fill="white"
          />
          <rect
            class="h-0 rect-2"
            width="4.72217"
            rx="2.36109"
            transform="matrix(0.569354 0.822092 -0.806982 0.590575 57.4912 0)"
            fill="white"
          />
        </svg>
      </div>
      <h4 class="modal-status">
        Completed!
        <div class="modal-status-line modal-status-line-1"></div>
        <div class="modal-status-line modal-status-line-2"></div>
      </h4>
      <p
        v-if="(response.status = 'Yay, we did it!!')"
        class="modal-message mb-3 xl:mb-9"
      >
        You are now number
        <span class="modal-number">{{ response.data.number }}</span> on the
        waiting list
      </p>
      <p class="modal-message">We will keep you updated</p>
      <button
        class="modal-cancel"
        aria-label="Click button to close modal"
        @click="setIsOpen(false)"
      >
        <svg
          width="38"
          height="38"
          viewBox="0 0 38 38"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M19.0016 19.0001L27.303 27.3016M10.7002 27.3016L19.0016 19.0001L10.7002 27.3016ZM27.303 10.6987L19 19.0001L27.303 10.6987ZM19 19.0001L10.7002 10.6987L19 19.0001Z"
            stroke="#BDBDBD"
            stroke-width="1.5"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </button>
    </Dialog>
  </section>
</template>

<style>
.modal {
  animation: modalAnim 0.3s ease-in-out forwards;
}
.modal-status-line {
  animation: lineAnim 0.5s ease-in-out forwards;
}
.modal-status-line-1 {
  animation-delay: 0.4s;
}
.modal-status-line-2 {
  animation-delay: 0.6s;
}
.rect-1 {
  animation: rect1Anim 0.5s 0.4s ease-in-out forwards;
}
.rect-2 {
  animation: rect2Anim 0.5s 0.4s ease-in-out forwards;
}
@keyframes modalAnim {
  from {
    opacity: 0;
    transform: translate(-50%, -30px);
  }
  to {
    opacity: 1;
    transform: translate(-50%, -50%);
  }
}
@keyframes lineAnim {
  to {
    width: 125px;
  }
}
@keyframes rect1Anim {
  to {
    height: 24.2795px;
  }
}
@keyframes rect2Anim {
  to {
    height: 58.0323px;
  }
}
</style>
