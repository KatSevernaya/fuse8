<template>
  <div class="catalog">
    <div class="catalog__wrap">
      <h1>Our Latest Developments</h1>
      <div class="catalog__filter">
        <label for="titleInput">Filter</label>
        <input
          type="text"
          id="titleInput"
          v-model="titleInput"
        >
      </div>
      <div class="catalog__list">
        <card
          v-for="item in catalog"
          :key="item.id"
          :cardData="item"
        >
        </card>
    </div>
    <div class="btn">
      See more
      <svg width="7" height="17" viewBox="0 0 7 17" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path id="Chevron" d="M1 1L5.043 8.41667L1 15.8333" stroke="#363636"
        stroke-width="2" stroke-linecap="round"/>
      </svg>
    </div>
    </div>
  </div>
</template>

<script>
import './assets/scss/style.scss';
import Card from './components/Card.vue';

export default {
  name: 'App',
  data() {
    return {
      catalogOrig: [],
      titleInput: '',
    };
  },
  computed: {
    catalog() {
      const filteredCat = [];
      let isFiltered = false;
      if (this.titleInput.length > 2) {
        isFiltered = true;
        this.catalogOrig.forEach((item) => {
          console.log(item.title.includes(this.titleInput));
          if (item.title.toLowerCase().includes(this.titleInput.toLowerCase())) {
            filteredCat.push(item);
          }
        });
        console.log(filteredCat);
      }
      return isFiltered ? filteredCat : this.catalogOrig;
    },
  },
  components: {
    Card,
  },
  mounted() {
    const requestURL = 'https://603e38c548171b0017b2ecf7.mockapi.io/homes';
    function sendRequest(method, url) {
      const headers = {
        'Content-Type': 'application/json',
      };
      return fetch(url, {
        method,
        headers,
      }).then((response) => {
        if (response.ok) {
          return response.json();
        }
        return response.json().then((error) => {
          const e = new Error('Something is wrong');
          e.data = error;
          throw e;
        });
      });
    }
    sendRequest('GET', requestURL)
      .then((data) => {
        this.catalogOrig = data;
        this.catalogOrig.forEach((element) => {
          const { id } = element;
          element.img = `http://lorempixel.com/350/150/city/${id}/`;
        });
        console.log(data);
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style lang="scss" scoped>
.catalog {
  background: #F2F2F2;
  margin: 0;
  min-height: 100vh;
  h1 {
    font-weight: bold;
    font-size: 36px;
    line-height: 49px;
    text-align: center;
    color: #45852D;
    margin: 0;
    margin-bottom: 43px;
    @media screen and (max-width: 785px) {
    font-size: 28px;
    line-height: 40px;
    margin-bottom: 22px;

  }
  }
}
.catalog__wrap {
  padding: 36px 38px 77px 50px;
  width: 100%;
  box-sizing: border-box;
   @media screen and (max-width: 785px) {
    padding: 18px 25px 38px 25px;
  }
}
.catalog__list {
  display: flex;
  margin-bottom: calc(60px - 22px);
  width: 100%;
  flex-wrap: wrap;
  @media screen and (max-width: 785px) {
    margin-bottom: calc(30px - 22px);
  }

}
.catalog__filter {
  margin-bottom: 45px;
  display: block;
  width: 100%;
  @media screen and (max-width: 785px) {
    margin-bottom: 22px;
  }
  input {
    height: 50px;
    border: 1px solid #D8D8D8;
    box-sizing: border-box;
    border-radius: 25px;
    width: 420px;
    max-width: calc(100% - 60px);
    padding-left: 20px;
    &:focus, &:active {
      outline: none;
      box-shadow: 0 0 10px 1px rgba(0,0,0, .1);

    }
    @media screen and (max-width: 1140px) {
        height: 40px;
    }
  }
  label {
    font-weight: bold;
    font-size: 16px;
    line-height: 24px;
    letter-spacing: -0.3px;
    margin-right: 15px;
  }

}
.btn {
  width: 150px;
  height: 50px;
  border: 1px solid #D8D8D8;
  box-sizing: border-box;
  border-radius: 25px;
  font-weight: bold;
  font-size: 16px;
  line-height: 24px;
  letter-spacing: -0.3px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  margin-left: auto;
  margin-right: auto;
  transition: all .2s ease-in;
  cursor: pointer;
  &:hover {
    box-shadow: 0 0 10px 1px rgba(0,0,0, .1);
  }
}
</style>
