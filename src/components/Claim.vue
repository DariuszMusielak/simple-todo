<template>
  <div v-bind:class="['claimWrapper loading']">
    <h1 class="header">
      <div class="header--small">simple</div>
      <div class="header--large">{{headerText}}</div>
      <div class="header--small">appcilation</div>
    </h1>
    <div class="descriptionWrapper">
      <p class="description">
        Simple todo application which makes your life easier.
      </p>
      <p class="description">
        Specify location, alerts, sync with google calendar and more.
      </p>
    </div>
  </div>

</template>
<script>
export default {
  name: 'Claim',
  props: {
    value: {
      type: Boolean,
      required: true,
    },
  },
  computed: {
    headerText: function call() {
      return this.value ? 'TODO' : 'YOUR TODOS';
    },
  },
};

</script>
<style lang="scss" scoped>
  .claimWrapper {
    display: flex;
    text-align: center;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background: #455A64;
    padding: 30px;
    color: #FFFFFF;
  }

  .loading {
    .header--small {
      font-size: 40px;
    }

    .description {
      font-size: 13px;
    }
    .descriptionWrapper {
      margin-top: 25px;
    }
  }

  .header--small, .description {
    transition: font-size .5s, margin-top .5s;
  }

  .header, .header--small, .header--large {
    margin: 0;
  }

  .header--large {
    font-size: 50px;
  }

  .header--small {
    font-size: 0;
    font-weight: 300;
  }

  .description {
    margin: 10px 0 0 0;
    font-size: 0;
  }

  .descriptionWrapper {
    margin-top: 0;
  }
</style>
