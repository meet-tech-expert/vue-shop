<template>
  <v-row class="my-10">
    <v-col
      cols="12"
      sm="2"
      md="3"
      class="products"
      :key="i"
      v-for="(item, i) in products"
    >
      <v-card class="mx-auto" outlined>
        <v-img class="main-image mt-3" height="230" :src="item.image"></v-img>
        <v-tooltip right color="#000">
          <template v-slot:activator="{ on, attrs }">
            <div class="heart-icon">
              <v-sheet color="transparent">
                <v-icon v-bind="attrs" v-on="on" color="#b70909" size="30px">
                  mdi-heart-outline
                </v-icon>
              </v-sheet>
            </div>
          </template>
          <span class="tooltip">הוסף לרשימת המשאלות</span>
        </v-tooltip>

        <v-card-title
          class="font-weight-bold subtitle-2 pb-1 px-1 justify-center name"
          >{{ item.name }}</v-card-title
        >

        <div class="title text-center font-weight-bold">₪{{ item.price }}</div>
        <v-card-actions class="justify-center">
          <v-btn class="cart-btn" width="90px">
            <span class="text">הוספה לסל</span>
            <v-icon small class="d-none">mdi-cart-outline</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
    <v-col class="my-5 footer">
      <infinite-loading
        :identifier="infiniteId"
        :distance="distanceHandle"
        @infinite="infiniteHandler"
        spinner="spiral"
      >
        <div slot="spinner" class="loader-message">
          <span>טוען עוד מוצרים...</span>
        </div>
        <div slot="no-more" class="loader-message">
          <span>כולכם נתפסים</span>
        </div>
        <div slot="no-results" class="loader-message">
          <span>מצטערים, עדיין אין מוצרים :(</span>
        </div>
        <div slot="error" class="loader-message">
          <span>אופס! משהו השתבש :(</span>
        </div>
      </infinite-loading>
    </v-col>
  </v-row>
</template>
<script>
import InfiniteLoading from "vue-infinite-loading";
export default {
  components: {
    InfiniteLoading,
  },
  data() {
    return {
      infiniteId: +new Date(),
      distanceHandle: 10,
      products: [
        {
          id: 1,
          name: "מספריים מקצועיים לגבות בצורת חסידה",
          price: 9.99,
          image:
            "https://www.beautycare.co.il/wp-content/uploads/2021/02/40042831-1-300x300.jpg",
        },
        {
          id: 2,
          name: "טופ קוט מאט ג’ל ללא צורך בניגוב STEP3",
          price: 10.99,
          image:
            "https://www.beautycare.co.il/wp-content/uploads/2021/06/1003260_72-300x300.jpg",
        },
        {
          id: 3,
          name: "ג’ל בסיס גמיש + גוון שלבים 1 + 2",
          price: 10.99,
          image:
            "https://www.beautycare.co.il/wp-content/uploads/2020/11/92021510-300x300.jpg",
        },
        {
          id: 4,
          name: "מכונת שיוף חשמלית מקצועית עם ראשי שיוף",
          price: 99.99,
          image:
            "https://www.beautycare.co.il/wp-content/uploads/2022/06/%D7%9E%D7%9B%D7%95%D7%A0%D7%AA-%D7%A9%D7%99%D7%95%D7%A3-%D7%9E%D7%A7%D7%A6%D7%95%D7%A2%D7%99%D7%AA-%D7%A4%D7%A8%D7%95%D7%A0%D7%98-4004262_72-300x300.jpg",
        },
      ],
    };
  },
  methods: {
    async infiniteHandler($state) {
      if (this.products.length <= 12) {
        this.products.push(...this.products);
        $state.loaded();
      } else {
        console.log("state.complete");
        $state.complete();
      }
    },
  },
};
</script>