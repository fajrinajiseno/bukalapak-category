<template>
    <div>
      <div class="row" v-bind:class="index % 2 == 0 ? 'white-bg' : 'grey-bg'" style="padding: 10px;">
        <div class="col-xs-1 plus-button" v-if="sub != null" @click="triggerActiveSub">
        </div>
        <div class="col-xs-1 minus-button" v-else @click="triggerDeactive">
        </div>
        <div class="col-xs-9 name">
          <a :href="url">
            {{name}}
          </a>
        </div>
        <div class="col-xs-2 count">
          {{count}}
        </div>
      </div>
      <wrappersubkategori
        v-if="sub != null"
        :name="name"
        :sub="sub"
        :active="activeSub"
        v-on:closed="triggerDeactive"
      ></wrappersubkategori>
    </div>
</template>

<script>
  export default {
    data() {
      return {
        activeSub: false,
      }
    },
    mounted() {
    },
    props: ['sub', 'name', 'count', 'url', 'index'],
    methods: {
      triggerActiveSub() {
        this.activeSub = true;
        this.$emit('opened');
      },
      triggerDeactive() {
        this.activeSub = false;
        this.$emit('closed');
      }
    }
  }
</script>
