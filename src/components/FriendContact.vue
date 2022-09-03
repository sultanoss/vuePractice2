<template>
  <li>
    <h2>{{ name }} {{ isFavorite ? '(Favorite)' : '' }}</h2>
    <button @click="showDetails()"
    >{{ detailsVisible ? 'Hide' : 'Show' }} Details
    </button>
    <button @click="isFriendFavorite()">favorite</button>
    <ul v-if="detailsVisible">
      <li><strong>Phone:</strong>{{ phoneNumber }}</li>
      <li><strong>Email:</strong>{{ emailAddress }}</li>
    </ul>
    <!--    here another way to bind emit event!-->
    <button @click="$emit('delete', id)">Delete Contact</button>
  </li>
</template>
<script>
export default {
  /*  props: [
      'name',
      'phoneNumber',
      'emailAddress',
    ],*/
  // emits: { another example using emits functions with condition as a function
  //   'is-FriendFavorite': function (id) {
  //     if (id) {
  //       return true;
  //     } else {
  //       console.warn('Id is missing')
  //       return false;
  //     }
  //   },
  // },

  props: {
    id: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    phoneNumber: {
      type: String,
      required: true,
    },
    emailAddress: {
      type: String,
      required: true,
    },
    isFavorite: {
      type: Boolean,
      required: false,
      default: false,
    }
  },
  emits: ['is-FriendFavorite', 'delete'],
  data() {
    return {
      detailsVisible: false,
    }
  }, methods: {
    showDetails() {
      this.detailsVisible = !this.detailsVisible;
    },
    isFriendFavorite() {
      this.$emit('change-favorite', this.id);
    },
  }
};
</script>