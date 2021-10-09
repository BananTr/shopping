<template>
  <v-app>
    <v-app-bar app color="#1B5E20" dark>
      <div class="d-flex align-center">
        <span> Gayetiyi </span>
      </div>

      <v-spacer></v-spacer>

      <v-btn href="" target="_blank" text @click="overlay = !overlay">
        <v-icon>mdi-cart</v-icon>
        <span class="numOfProduct"> {{ totalProduacts }}</span>
      </v-btn>

      <div class="cart" v-show="overlay">
        <v-btn text @click.stop="overlay = false" color="#1B5E20">
          <v-icon>mdi-close</v-icon>
        </v-btn>
        <v-card
          v-for="product in products"
          :key="product.id"
          class="mx-auto"
          outlined
        >
          <v-list-item three-line>
            <v-list-item-content>
              <div class="text-overline mb-1">
                {{ product.name }}
              </div>
              <v-list-item-title class="text mb-1">
                Quantity : {{ product.quantity }}
              </v-list-item-title>
            </v-list-item-content>
            <v-list-item-avatar tile size="80"
              ><v-img :src="product.img"></v-img
            ></v-list-item-avatar>
          </v-list-item>
        </v-card>
      </div>
    </v-app-bar>
    <v-main>
      <v-container>
        <v-row class="text-center">
          <v-col cols="12">
            <v-card
              :loading="loading"
              class="mx-auto my-12"
              max-width="374"
              v-for="product in products"
              :key="product.id"
            >
              <template slot="progress">
                <v-progress-linear
                  color="deep-purple"
                  height="10"
                  indeterminate
                ></v-progress-linear>
              </template>
              <v-card-title>{{ product.name }}</v-card-title>
              <v-img
                height="250"
                ma-2
                :src="product.img"
                :alt="product.name"
              ></v-img>

              <v-card-text>
                <div class="my-4 text-subtitle-1">
                  {{ product.description }}
                </div>
                <div class="my-4 text-subtitle-1">{{ product.price }} $</div>
              </v-card-text>
              <v-card-actions>
                <v-btn
                  color="deep-purple lighten-2"
                  text
                  @click="
                    product.quantity > 0
                      ? product.quantity--
                      : (product.quantity = 0)
                  "
                >
                  <v-icon dark> mdi-minus </v-icon>
                </v-btn>
                <v-card-text>
                  <span> {{ product.quantity }}</span>
                </v-card-text>
                <v-btn
                  color="deep-purple lighten-2"
                  text
                  @click="product.quantity++"
                >
                  <v-icon dark> mdi-plus </v-icon>
                </v-btn>
              </v-card-actions>
              <v-card-actions>
                <v-btn color="deep-purple lighten-2" text @click="addToCart">
                  + <v-icon dark> mdi-cart </v-icon>
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    overlay: false,
    products: [
      {
        id: 1,
        name: "peanut",
        price: 50,
        quantity: 0,
        img: "https://toplasepeti.com/wp-content/uploads/2020/07/f%C4%B1st%C4%B1kezmesi2.jpg",
        description: "lorem opes",
      },
      {
        id: 2,
        name: "tea",
        price: 50,
        quantity: 0,
        img: "https://m.media-amazon.com/images/I/51dE378i-zL._SL1000_.jpg",
        description: "lorem lacosta",
      },
      {
        id: 3,
        name: "coconut",
        price: 50,
        quantity: 0,
        img: "https://productimages.hepsiburada.net/s/37/1500/10544331849778.jpg",
        // img:"../assets/coconut.jpg",
        description: "lorem va la bane",
      },
    ],
  }),
  computed: {
    totalProduacts() {
      return this.products.reduce(
        (total, product) => total + product.quantity,
        0
      );
    },
    cart() {
      return this.products.filter((product) => product.quantity > 0);
    },
  },
};
</script>
<style scoped>
.cart {
  width: auto;
  background: rgb(252, 251, 251);
  border: 1px solid rgb(206, 202, 202);
  border-radius: 1px;
  margin-top: 500px;
  position: absolute;
}
.theme--dark.v-card {
  background-color: #fffdfd;
  color: #ffffff;
}

.theme--dark.v-list-item:not(.v-list-item--active):not(.v-list-item--disabled) {
  color: #240505 !important;
  font-size: bold;
}
.numOfProduct {
  background-color: #fff;
  color: #1b5e20;
  padding: 0.1rem;
  border: 1px solid #1b5e20;
  border-radius: 50% 20%;
}
</style>