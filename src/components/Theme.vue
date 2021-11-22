<template>
  <div class="container">
    <div>
      <img src="../assets/noiva.png" alt="noivo" />
    </div>
    <div class="toggle">
      <input id="switch" type="checkbox" name="theme" @change="onTheme" />
      <label for="switch">Toggle</label>
    </div>
    <div>
      <img src="../assets/noivo.png" alt="noivo" />
    </div>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      thema: false,
    };
  },

  mounted() {
    this.onTheme();
  },
  methods: {
    defineThema() {
      if (isTheme) {
        this.thema = isTheme;
        document.getElementById("switch").checked = true;
      } else {
        isTheme = [this.thema];
        localStorage.setItem("themaStorage", isTheme);
        document.getElementById("switch").checked = false;
        this.onTheme();
      }
    },
    onTheme() {
      const html = document.querySelector("html");
      let checkbox = document.querySelector("input[name=theme]");

      const getStyle = (element, style) => {
        return window.getComputedStyle(element).getPropertyValue(style);
      };

      const noivaTheme = {
        bgRosaPadrao: getStyle(html, "--bg-rosa-padrao"),
        bgDark: getStyle(html, "--bg-dark"),
        bgCard: getStyle(html, "--bg-card"),
        bg: getStyle(html, "--bg"),
        bgTitle: getStyle(html, "--bg-title"),
        bgFonte: getStyle(html, "--bg-fonte"),
        bgBotao: getStyle(html, "--bg-botao"),
        bgBtnCardPremium: getStyle(html, "--bg-btn-card-premium"),
        bgCorpoCardPremium: getStyle(html, "--bg-corpo-card-premium"),
        bgCardIcon: getStyle(html,"--bg-card-icon"),
        bgCardIconTop: getStyle(html, "--bg-card-icon-top"),
      };

      const noivoTheme = {
        bgRosaPadrao: "#292b2c",
        bgDark: "#292b2c",
        bgCard: `linear-gradient(to bottom, hsl(224, 36%, 15%), hsl(224, 36%, 15%))`,
        bg: "hsl(223, 31%, 20%)",
        bgTitle: "white",
        bgFonte: "white",
        bgBotao: `linear-gradient(to bottom, white, white, white)`,
        bgCardIcon: `invert(100%) sepia(100%) saturate(100%) hue-rotate(100deg) brightness(100%) contrast(100%)`,
      };

      const transformKey = (key) => {
        return "--" + key.replace(/([A-Z])/g, "-$1").toLowerCase();
      };

      const changeColors = (colors) => {
        Object.keys(colors).map((key) =>
          html.style.setProperty(transformKey(key), colors[key])
        );
      };
      checkbox.addEventListener("change", ({ target }) => {
        target.checked ? changeColors(noivoTheme) : changeColors(noivaTheme);
      });
    },
  },
};
</script>


<style scoped>
.container {
  display: flex;
  width: 500px;
  justify-content: flex-end;
  align-items: baseline;
}

img {
  width: 30px;
  height: 30px;
}

input[type="checkbox"] {
  height: 0;
  width: 0;
  visibility: hidden;
}

label {
  cursor: pointer;
  text-indent: -9999px;
  width: 52px;
  height: 27px;
  background: #ff6f9c;
  float: right;
  border-radius: 100px;
  position: relative;
}

label::after {
  content: "";
  position: absolute;
  top: 3px;
  left: 3px;
  width: 20px;
  height: 20px;
  background-color: white;
  border-radius: 90px;
  transition: 0.3s;
}

input:checked + label {
  background-color: #2b2b2b;
}

input:checked + label::after {
  left: calc(100% - 5px);
  transform: translateX(-100%);
}

label:active:after {
  width: 45px;
}

@media (max-width: 500px) {
    .container{
        width: 100%;
        padding-right: 10px;
    }
    
}
</style>