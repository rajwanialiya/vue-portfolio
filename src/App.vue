<template>
  <div id="app">
    <router-view></router-view>
    <div class="circle">
      <h5 class="next-text">Next</h5>
      <h5 class="prev-text">Prev</h5>
    </div>
  </div>
</template>

<script>
// https://www.kirupa.com/canvas/follow_mouse_cursor.htm
export default {
  name: "app",
  data() {
    return {};
  },
  mounted: function() {
    document.addEventListener("mousemove", ev => this.cursorMove(ev));
  },
  methods: {
    cursorMove: function(ev) {
      var circle = document.querySelector(".circle");
      var next = document.querySelector(".next-text");
      var prev = document.querySelector(".prev-text");
      let posY = ev.clientY;
      let posX = ev.clientX;

      circle.style.top = posY + "px";
      circle.style.left = posX + "px";
      prev.style.display = "none";
      next.style.display = "none";

      circle.style.height = "15px";
      circle.style.width = "15px";

      if (
        ev.target.tagName === "A" ||
        (ev.target.firstChild && ev.target.firstChild.tagName === "A") ||
        ev.target.className === "a" ||
        (ev.target.parentNode && ev.target.parentNode.tagName === "A")
      ) {
        circle.style.transform = "scale(2) perspective(1px)";
      } else {
        circle.style.transform = "scale(1) perspective(1px)";
      }

      if (
        ev.target.classList.value === "next-proj" ||
        ev.target.classList.value === "prev-proj"
      ) {
        circle.style.width = "80px";
        circle.style.height = "80px";
        if (ev.target.classList.value === "prev-proj") {
          prev.style.display = "block";
          next.style.display = "none";
        } else if (ev.target.classList.value === "next-proj") {
          prev.style.display = "none";
          next.style.display = "block";
        }
      }
    }
  }
};
</script>

<style>
#app {
  cursor: none;
}

body {
  line-height: 1.7em;
}

a {
  z-index: 10;
}

a:hover {
  cursor: none;
}

.fp-tableCell {
  display: flex;
  justify-content: center;
  align-items: center;
}

.view-wrap {
  width: 100vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.view-content {
  max-width: 1050px;
  margin: 0 0;
  overflow: hidden;
}

.section {
  width: 100vw;
  height: 100vh;
}

.dropdown-menu {
  border: solid 0.08rem black;
  background-color: rgba(
    255,
    255,
    255,
    0.7
  ) !important; /* Semi-transparent white background */
  backdrop-filter: blur(
    15px
  ) !important; /* Blurs the background behind the navbar */
  -webkit-backdrop-filter: blur(7px) !important; /* Safari support */
}

h2,
h3,
h4,
h5,
h6,
p {
  margin-bottom: 0.5em;
}

router-link,
a,
a:hover {
  text-decoration: none;
  color: black;
}

.circle {
  position: fixed;
  border-radius: 50%;
  z-index: 4000;
  height: 15px;
  width: 15px;
  pointer-events: none;
  transition: background ease-in 10ms, box-shadow ease-in 150ms,
    transform ease-in 150ms;
  transform: translate3d(0, 0, 0);
  background-color: transparent;
  aborder: 2px solid black;
  box-shadow: 0 0 0 2px black;
  display: flex;
  justify-content: center;
  align-items: center;
}

.next-text,
.prev-text {
  display: none;
  cursor: none;
  margin: 0;
  color: black;
}
/* .hover {
  width: 25px;
  height: 25px;
} */

/* a:hover {
  cursor: none;
} */

/* SMALL */
@media screen and (max-width: 576px) {
  #app {
    overflow: hidden;
  }

  .view-content {
    min-height: 80vh;
    margin: 30px 0;
  }
}

@media screen and (max-width: 950px) {
  .section,
  .fp-tableCell,
  .fp-section,
  .fp-table {
    height: auto !important;
    margin: 30px 0;
  }
}
</style>
