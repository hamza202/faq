<template>
  <div class="faq-page container">
    <div class="text-center">
      <h3>FAQ</h3>
    </div>
    <b-card no-body class="">
      <b-tabs pills card :vertical="vertical">
        <b-tab class=""
          v-for="(category, categoryIndex) in faqs"
          :key="categoryIndex"
          :title="category.Name"
          ><b-card-text>
            <div class="accordion" role="tablist">
              <b-card
                v-for="faq in category.Questions"
                :key="faq.Priority"
                no-body
                class=""
              >
                <b-card-header header-tag="header" class="p-1" role="tab">
                  <b-button
                    block
                    v-b-toggle="'faq' + faq.Priority"
                    variant="info"
                    >{{ faq.Title }}</b-button
                  >
                </b-card-header>
                <b-collapse
                  :id="'faq' + faq.Priority"
                  accordion="my-accordion"
                  role="tabpanel"
                >
                  <b-card-body>
                    <b-card-text>{{ faq.Body }}</b-card-text>
                    <div>
                      <b-button
                        variant="useful-btn"
                        @click="changeUseful(faq.Priority)"
                        >useful</b-button
                      >
                      <b-button variant="useful-btn">not useful</b-button>
                    </div>
                  </b-card-body>
                </b-collapse>
              </b-card>
            </div>
          </b-card-text></b-tab
        >
      </b-tabs>
    </b-card>
  </div>
</template>

<script>
// @ is an alias to /src
import Faqs from "@/data.json";
export default {
  name: "Faq",

  data() {
    return {
      faqs: [],
      size: 0
    };
  },
  computed: {
    vertical() {
      if (this.size > 900) return true;
      return false;
    },
  },
  methods: {
    changeUseful(id) {
      const Useful = localStorage.getItem("Useful");
      if (Useful) {
        const parseJson = Useful;
      }
      var house = street.houses.find((h) =>
        h.rooms.some((r) => r.id === roomId)
      );
    },
    changeUnUseful(id) {
      var house = street.houses.find((h) =>
        h.rooms.some((r) => r.id === roomId)
      );
    },
  },
  mounted() {
    this.faqs = Faqs;
    console.log(Faqs);
    var that = this;
    that.size = window.innerWidth;
    window.onresize = function () {
      that.size = window.innerWidth;
    };
  },
};
</script>
