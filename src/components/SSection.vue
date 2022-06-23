<template>
  <section class="service-section" ref="section">
    <header
      class="section-header"
      :data-index="index + 1"
      :style="
        !section.paragraphs || section.paragraphs.length == 0
          ? 'height: 100%'
          : ''
      "
    >
      <figure>
        <img :src="section.poster" :alt="section.name" class="poster" />
        <img :src="section.icon" :alt="section.name" class="icon" />
      </figure>
      <h3>{{ section.name }}</h3>
      <p class="extended-p">
        {{ section.description }}
      </p>
      <p class="short-p">
        {{ `${section.description.slice(0, 110)}...` }}
      </p>
      <m-button class="slide-button" @click="extend($event, true)">
        اقرأ أكثر
      </m-button>
      <button
        class="close"
        @click="extend($event, false)"
        v-if="!section.paragraphs || section.paragraphs.length == 0"
      >
        <i class="fas fa-times"></i>
      </button>
    </header>
    <article
      class="section-body"
      v-if="section.paragraphs && section.paragraphs.length > 0"
    >
      <button class="close" @click="extend($event, false)">
        <i class="fas fa-times"></i>
      </button>
      <div
        v-for="(paragraph, index) in section.paragraphs"
        :key="`${section.name}-paragraph-${index}`"
        v-html="paragraph"
      ></div>
    </article>
  </section>
</template>

<script>
export default {
  name: "SSection",
  props: {
    section: Object,
    index: Number,
  },
  methods: {
    extend(e, decision) {
      if (decision) {
        if (e.currentTarget.nodeName == "BUTTON") {
          e.currentTarget.parentElement.parentElement.classList.add("extended");
        } else {
          e.currentTarget.classList.add("extended");
        }
      } else {
        if (e.currentTarget.nodeName == "BUTTON") {
          e.currentTarget.parentElement.parentElement.classList.remove(
            "extended"
          );
        } else {
          e.currentTarget.classList.remove("extended");
        }
      }
    },
  },
};
</script>

<style lang="scss">
section.service-section {
  transform: translateX(calc(var(--step-amount) * var(--current-step)));
  height: 100vh;
  width: 340px;
  max-width: 100%;
  flex-shrink: 0;
  color: white;
  transition: all 0.8s ease;
  border-left: 2px solid rgba(255, 255, 255, 0.05);
  overflow: hidden;
}
//   Section Header
header.section-header {
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: center;
  padding: 40px 10px;
  height: 100vh;
  transition: height 0.2s ease;
  position: relative;
  button.close {
    display: none;
  }
  &::after {
    content: "";
    position: absolute;
    top: 0;
    right: 0;
    width: 100%;
    height: 100%;
    background-image: linear-gradient(
      60deg,
      transparent 0%,
      rgba(255, 255, 255, 0.3) 100%
    );
    opacity: 0;
    transition: opacity 0.2s ease;
    z-index: 2;
  }
  &::before {
    content: attr(data-index);
    position: absolute;
    top: 20px;
    right: 10px;
    z-index: 1;
  }
  figure {
    margin: 0;
    padding: 0;
    position: relative;
    img {
      width: 100%;
      max-width: 400px;
      margin: 20px 0;
      z-index: 3;
      transition: opacity 0.4s ease-out;
      &.poster {
        opacity: 0;
      }
      &.icon {
        width: 80px;
        position: absolute;
        margin: auto auto;
        top: 50%;
        right: 50%;
        transform: translate(50%, -50%);
      }
    }
  }
  &:hover {
    &::after {
      opacity: 1;
    }
    img {
      &.poster {
        opacity: 1;
      }
      &.icon {
        opacity: 0;
      }
    }
  }
  h3 {
    height: 50px;
  }
  p {
    width: 90%;
    max-width: 1000px;
    font-size: 0.8em;
    color: var(--accent);
    line-height: 1.6em;
    margin: 0 auto;
    height: 100px;
    overflow: hidden;
    &.extended-p {
      display: none;
    }
    &.short-p {
      display: block;
    }
  }
}
//   Section Body
article.section-body {
  width: 100%;
  text-align: right;
  background: $color_main;
  color: $color_text;
  display: none;
  position: relative !important;
  div {
    padding: 20px;
  }
  p {
    max-width: 1000px;
  }
}

// Extended Section
section.extended {
  border: 1px solid $color_text;
  overflow: auto;
  header.section-header {
    height: 90%;
    &::before {
      display: none;
    }
    p {
      height: auto;
      white-space: normal;
      &.extended-p {
        display: block;
      }
      &.short-p {
        display: none;
      }
    }
  }
  article.section-body {
    display: block;
  }
  transform: translateX(var(--far-from-start));
  width: 100vw;
  max-width: none;
  //   height: 100%;
  background-color: #27153d;
  z-index: 4;
  display: block;
  &::before {
    opacity: 0;
  }
  button.close {
    display: block;
  }
  button.slide-button {
    display: none;
  }
  img {
    &.poster {
      opacity: 1 !important;
    }
    &.icon {
      opacity: 0 !important;
    }
  }
}
</style>
