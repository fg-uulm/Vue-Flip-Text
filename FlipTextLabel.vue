<template>
  <span class="label">
    {{textRendered}}
  </span>
</template>

<script>
export default {
  name: 'HeaderBar',
  props: {
    text:  {
        type: String,
        default: "I'm a label",
    },
    chance: {
        type: Number,
        default: 0.05,
    },
    time: {
        type: Number,
        default: 30,
    }
  },
  data: function () {
    return {
        textRendered: "",
        garbleInterval: -1,
    }
  },
  methods: {
        replaceAt: function (s, n, t) {
                return s.substring(0, n) + t + s.substring(n + 1);
        }
  },
  watch: {
        text: {
            immediate: true,
            handler: function () { // watch it
                clearInterval(this.garbleInterval);

                this.textRendered = "";
                //create initial garble string
                for (var i = 0; i < this.text.length; i++) {
                    if (this.text.charAt(i) != " ") {
                        this.textRendered += Math.random().toString(36).substr(2, 1);
                    } else {
                        this.textRendered += " ";
                    }
                }

                this.garbleInterval = setInterval(() => {
                    //by chance add either real char or another random
                    for (var i = 0; i < this.text.length; i++) {
                        if (this.text.charAt(i) != " " && this.text.charAt(i) != this
                            .textRendered.charAt(i)) {
                            if (Math.random() > this.chance) {
                                //another random
                                this.textRendered = this.replaceAt(this.textRendered, i, Math
                                    .random().toString(36).substr(2, 1));
                            } else {
                                //the real one
                                this.textRendered = this.replaceAt(this.textRendered, i, this
                                    .text.charAt(i));
                            }
                        }
                    }
                    //end condition reached                
                    if (this.textRendered == this.text) clearInterval(this.garbleInterval);
                }, this.time)
            }
        }
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
