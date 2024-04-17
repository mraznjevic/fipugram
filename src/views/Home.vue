<template>
    <div class="row">
        <div class="col-8">
            <instagram-card v-for="card in filteredCards" :key="card.url" :info="card" />
        </div>
        <div class="col-4">
            Sidebar
        </div>
    </div>
</template>
<script>
// @ is an alias to /src
import InstagramCard from '@/components/InstagramCard.vue';
import store from '@/store';

let cards = [];

cards = [
 { url: require('@/assets/images/sunset1.jpg'), description: 'evening sunset', time: 'few minutes ago...'},
 { url: require('@/assets/images/sunset2.jpg'), description: 'nature sunset', time: 'hour ago...'},
 { url: require('@/assets/images/sunset3.jpg'), description: 'mountain sunset', time: 'few hours ago...'},
 { url: require('@/assets/images/sunset4.jpg'), description: 'relax moments', time: '9 hours ago...'},
];

export default {
  name: 'home',
  data: function(){
    return{
          cards:cards,
          store:store,
    };
  },

  computed: {
    filteredCards() {
      let termin=this.store.searchTerm;
    return this.cards.filter(card => card.description.indexOf(termin)>=0);
    },
  },



  components: {
    InstagramCard: InstagramCard,
  },
};
</script>

  