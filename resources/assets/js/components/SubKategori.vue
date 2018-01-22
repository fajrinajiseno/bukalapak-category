<template>
    <div>
      <div class="row sub-category-row">
        <div class="col-xs-1 plus-button" v-if="sub != null" @click="triggerActiveSubSub">
        </div>
        <div class="col-xs-1 minus-button" v-else @click="triggerDeactiveSub">
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
      <wrappersubsubkategori
        v-if="sub != null"
        :name="name"
        :sub="sub"
        :active="activeSubSub"
        v-on:closedPanel="triggerDeactiveSubSub"
      ></wrappersubsubkategori>
    </div>
</template>

<script>
  export default {
    data() {
      return {
        activeSubSub: false
      }
    },
    mounted() {
    },
    props: ['sub', 'name', 'count', 'url'],
    methods: {
      triggerActiveSubSub() {
        this.activeSubSub = true;
        this.$emit('opened');
      },
      triggerDeactiveSub() {
        this.$emit('closed');
      },
      triggerDeactiveSubSub() {
        this.activeSubSub = false;
        this.$emit('closedPanel');
      }
    },
  }
</script>
