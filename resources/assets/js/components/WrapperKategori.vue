<template>
    <div class="row">
        <div class="col-md-12">
          <div class="panel-wrapper">
            <div class="panel-title">
              <div class="col-xs-2">
              </div>
              <div class="col-xs-8">
                <div class="logo">
                </div>
              </div>
              <div class="col-xs-2">
                <div class="refresh" @click="refreshPage">
                </div>
              </div>
            </div>
            <div class="panel panel-default main" ref="main" :class="{ closed: activePanel }">
                <div class="panel-heading darker-grey-bg">Pilih Kategori:</div>
                  <div class="panel-body">
                    <kategori
                      v-for="(data, index) in myJson"
                      :key="index"
                      :index="index"
                      :name="data.name"
                      :sub="data.sub"
                      :url="data.url"
                      :count="data.count"
                      v-on:opened="triggerActive"
                      v-on:closed="triggerDeactive"
                    ></kategori>
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
        myJson: require('../../json/main.json').categories,
        activePanel : false,
      }
    },
    mounted() {
      // this.sortedArray();
    },
    props: [],
    methods: {
      triggerActive() {
        this.activePanel = true;
        this.$nextTick(() => {
          this.$refs.main.scrollTop = 0;
        })
      },
      triggerDeactive() {
        this.activePanel = false;
      },
      refreshPage() {
        location.reload();
      }
    }
  }
</script>
