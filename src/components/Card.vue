<template>
  <a class="card" :href="href">
    <div class="card__img">
      <img :src="cardData.img" alt="">
      <div class="card__type"
      :class="{
        'blue' : cardData.type == 'IndependentLiving',
        'orange' : cardData.type == 'SupportAvailable'
        }"
      >
        <p>{{ type }}</p>
      </div>
    </div>
    <div class="card__content">
      <h2>{{ cardData.title }}</h2>
      <p class="adress">{{ cardData.address }}</p>
      <p class="price">New Properties for Sale from <span>£{{ price }}</span></p>
      <p class="text">Shared Ownership Available</p>
    </div>
  </a>
</template>
<script>
export default {
  props: ['cardData'],
  data() {
    return {
      price: '',
      type: '',
      href: '',
    };
  },
  mounted() {
    this.price = this.cardData.price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
    this.href = `https://www.someamazingtitle.com/details/${this.cardData.id}`;
    if (this.cardData.type === 'SupportAvailable') {
      this.type = 'Restaurant & Support available';
    } else {
      this.type = 'Independent living';
    }
  },
};
</script>
<style lang='scss'>
.card {
  width: calc((100% - 24px * 3) / 3);
  background: #F8F8F8;
  border: 1px solid #D8D8D8;
  margin-bottom: 38px;
  margin-right: 22px;
  text-decoration: none;
  color: #363636;
  justify-content: space-between;
  transition: all .3s ease-in;
  @media screen and (max-width: 1140px) {
    width: calc((100% - 24px * 2) / 2);
  }
  @media screen and (max-width: 785px) {
    width: 100%;
    margin-right: 0;
    margin-bottom: 20px;
  }
  &:hover {
    box-shadow: 0 0 10px 5px rgba(0,0,0, .2);
  }
}
.card__img {
  width: 100%;
  position: relative;
  img {
    width: 100%;
  }
}
.card__content {
  padding: 20px 17px;
  h2 {
    font-weight: bold;
    font-size: 20px;
    line-height: 27px;
    margin-top: 0;
    margin-bottom: 2px;
  }
  .adress {
    font-size: 16px;
    line-height: 22px;
    margin-bottom: 15px;
  }
  .price {
    font-size: 16px;
    line-height: 22px;
    margin-bottom: 7px;
    span {
      font-weight: bold;
    }
  }
  .text {
    font-size: 14px;
    line-height: 19px;
  }

}
.blue {
    background: #006F79;
  }
  .orange {
    background: #EC6608;
  }
.card__type {
  position: absolute;
  bottom: 5px;
  right: 0;
  color: #FFFFFF;
  padding: 8px 8px 5px;
  p {
    margin: 0;
    font-weight: bold;
    font-size: 12px;
    line-height: 16px;
  }
}
</style>
