<template>
  <div class="container text-center">
    <div class="row">
      <div
        v-for="(card, index) in cards"
        :key="index"
        class="col card"
        @click="openModal(card)"
      >
        <h5 class="card-title">{{ card.title }}</h5>
        <p class="card-text">{{ card.text }}</p>
        <a href="#" class="btn btn-primary" @click.stop.prevent="openModal(card)">{{ card.buttonText }}</a>
      </div>
    </div>
  </div>

  <!-- Modal: displays the clicked card -->
  <div
    ref="cardModal"
    class="modal fade"
    id="exampleModal"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="exampleModalLabel">{{ selectedCard.title || 'Details' }}</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <div class="card" style="width: 100%;">
            <img v-if="selectedCard.image" :src="selectedCard.image" class="card-img-top" :alt="selectedCard.title || 'image'">
            <div class="card-body">
              <h5 class="card-title">{{ selectedCard.title }}</h5>
              <p class="card-text">{{ selectedCard.text }}</p>
            </div>
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
          <button type="button" class="btn btn-primary">Save changes</button>
        </div>
      </div>
    </div>
  </div>
</template>






<script>
export default {
  data() {
    return {
      cards: [
        {
          title: 'Card One',
          text: 'With supporting text below as a natural lead-in to additional content.',
          image: 'https://via.placeholder.com/600x300',
          buttonText: 'Explore'
        },
        {
          title: 'Card Two',
          text: 'With supporting text below as a natural lead-in to additional content.',
          image: 'https://via.placeholder.com/600x300?text=Two',
          buttonText: 'Learn More'
        },
        {
          title: 'Card Three',
          text: 'With supporting text below as a natural lead-in to additional content.',
          image: 'https://via.placeholder.com/600x300?text=Three',
          buttonText: 'Discover'
        }
      ],
      selectedCard: {},
      bsModal: null
    }
  },
  methods: {
    openModal(card) {
      this.selectedCard = card || {};
      if (window.bootstrap && this.$refs.cardModal) {
        if (!this.bsModal) this.bsModal = new window.bootstrap.Modal(this.$refs.cardModal);
        this.bsModal.show();
      }
    }
  },
  mounted() {
    if (window.bootstrap && this.$refs.cardModal) {
      this.bsModal = new window.bootstrap.Modal(this.$refs.cardModal);
    }
  },
  beforeUnmount() {
    if (this.bsModal) {
      this.bsModal.dispose();
      this.bsModal = null;
    }
  }
}
</script>




<style>
.row {
  display: flex;
  margin: 20px;
  gap: 20px;
  justify-content: center;
  flex-wrap: wrap;
}

.card {
  border: 2px solid #007bff;
  border-radius: 8px;
  padding: 20px;
    background-color: white;
  transition: all 0.3s ease;
  cursor: pointer;
}

.card:hover {
  border-color: #0056b3;
  box-shadow: 0 4px 12px rgba(0, 86, 179, 0.3);
  transform: translateY(-5px);
}

.card-title {
  color: #333;
  font-weight: 600;
  margin-bottom: 10px;
}

.card-text {
  color: #666;
  font-size: 14px;
  margin-bottom: 15px;
}
</style>