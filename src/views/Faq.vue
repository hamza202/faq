<template>
  <div class="faq-page container">
    <div class="text-center">
      <h3>FAQ</h3>
    </div>
    <b-card no-body class="">
      <b-tabs pills card :vertical="vertical">
        <b-tab
            class=""
            v-for="(category, categoryIndex) in faqs"
            :key="categoryIndex"
            :title="category.Name"
        ><b-card-text>
          <div class="accordion" role="tablist">
            <b-card
                v-for="(faq, faqIndex) in category.Questions"
                :key="`${faq.Priority} - ${faqIndex}`"
                no-body
                class=""
            >
              <b-card-header header-tag="header" class="p-1" role="tab">
                <b-button
                    block
                    v-b-toggle="'faq' + faqIndex + faq.Priority"
                    variant="info"
                >
                  {{ faq.Priority + " - " + faq.Title }}</b-button
                >
              </b-card-header>
              <b-collapse
                  :id="'faq' + faqIndex + faq.Priority"
                  accordion="my-accordion"
                  role="tabpanel">
                <b-card-body>
                  <b-card-text>{{ faq.Body }}</b-card-text>
                  <div>
                    <b-button variant="useful-btn">useful</b-button>
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
      size: 0,
    };
  },
  computed: {
    vertical() {
      if (this.size > 900) return true;
      return false;
    },
  },
  methods: {
    dynamicSort(property) {
      var sortOrder = 1;
      if (property[0] === "-") {
        sortOrder = -1;
        property = property.substr(1);
      }
      return function (a, b) {
        var result =
            a[property] < b[property] ? -1 : a[property] > b[property] ? 1 : 0;
        return result * sortOrder;
      };
    },
  },
  mounted() {
    const faqs = Faqs;

    this.faqs = faqs.sort(this.dynamicSort("Priority"));

    const dataFaqs = this.faqs
    for (let faqsIndex = 0; faqsIndex < dataFaqs.length; faqsIndex++) {
      const Questions = dataFaqs[faqsIndex].Questions;
      Questions.sort(this.dynamicSort("Priority"));
      this.faqs[faqsIndex].Questions = Questions;
    }

    var that = this;
    that.size = window.innerWidth;
    window.onresize = function () {
      that.size = window.innerWidth;
    };
  },
};
</script>
