<template>
    <div class="row" v-if="activeSubSub">
        <div>
            <div class="panel panel-default sub-category" :class="{ 'close-animation': closeAnimation }" id="subsubkategori">
                <div class="panel-heading darker-grey-bg">Pilih Subkategori {{name}}: <div class="close-category" style="float:right" @click="triggerDeactiveSubSub"></div></div>
                <div class="panel-body">
                  <div class="row sub-category-row"v-for="(data, index) in myJson">
                    <div class="col-xs-1 minus-button" @click="triggerDeactiveSubSub">
                    </div>
                    <div class="col-xs-9 name">
                      <a :href="data.url">
                        {{data.name}}
                      </a>
                    </div>
                    <div class="col-xs-2 count">
                      {{data.count}}
                    </div>
                  </div>
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
        activeSubSub: this.active,
        closeAnimation: false,
      }
    },
    mounted() {
    },
    props: ['sub', 'name', 'active'],
    methods: {
      triggerDeactiveSubSub() {
        this.closeAnimation = true;
        setTimeout( () => {
          this.activeSubSub = false;
          this.$emit('closedPanel');
          this.closeAnimation = false;
        }, 300);
      }
    },
    watch: {
      active: function(newVal, oldVal) {
        this.activeSubSub = newVal;
      }
    }
  }
</script>
