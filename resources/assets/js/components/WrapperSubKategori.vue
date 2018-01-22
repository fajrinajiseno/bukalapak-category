<template>
    <div class="row" v-if="activeSub">
        <div>
            <div class="panel panel-default sub-category" ref="subkategori" id="subkategori" :class="{ closed: activePanel, 'close-animation': closeAnimation }">
                <div class="panel-heading darker-grey-bg">Pilih Subkategori {{name}}: <div class="close-category" style="float:right" @click="triggerDeactiveSub"></div></div>
                <div class="panel-body">
                  <subkategori
                    v-for="(data, index) in myJson"
                    :key="index"
                    :name="data.name"
                    :sub="data.sub"
                    :url="data.url"
                    :count="data.count"
                    :active="active"
                    v-on:opened="triggerActive"
                    v-on:closed="triggerDeactiveSub"
                    v-on:closedPanel="triggerDeactiveSubSub"
                  ></subkategori>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
  export default {
    data() {
      return {
        myJson: require('../../json/'+this.sub).categories,
        activeSub: this.active,
        activePanel:false,
        closeAnimation: false,
      }
    },
    mounted() {
      // this.sortedArray();
    },
    props: ['sub', 'name', 'active'],
    methods: {
      triggerActive() {
        this.activePanel = true;
        this.$nextTick(() => {
          this.$refs.subkategori.scrollTop = 0;
        })
      },
      triggerDeactiveSub() {
        this.closeAnimation = true;
        setTimeout( () => {
          this.activeSub = false;
          this.$emit('closed');
          this.closeAnimation = true;
        }, 300);
      },
      triggerDeactiveSubSub() {
        this.activePanel = false;
      }
    },
    watch: {
      active: function(newVal, oldVal) {
        this.activeSub = newVal;
      },
    }
  }
</script>
