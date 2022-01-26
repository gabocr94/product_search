<template src="./productDisplayTemplate.html"></template>
<script>
import "./productDisplayStyle.css";
import "bootstrap/dist/css/bootstrap.css";
import "@fortawesome/fontawesome-free/js/all.js";
import products from "./products.json";
export default {
  setup() {},
  data() {
    return {
      product_list: products,
      search: "",
      quantities: {}
    };
  },
  methods: {
    find() {
      this.product_list = [];
      let searchTxt = this.search.toUpperCase();
      if (searchTxt == "") {
        this.product_list = products
      } else {
        products.forEach((element) => {
          if (
            element.product.toUpperCase() == searchTxt ||
            element.item_code.toUpperCase() == searchTxt ||
            element.category.toUpperCase() == searchTxt
          ) {
            this.product_list.push(element);
          }
        });
      }
    },

    updateQty(item_id){
        this.product_list.forEach((element, counter) => {
            if(element.id == item_id){
                element.units = this.quantities[item_id];
                this.product_list[counter] = element;
            }
        })
    }
  },
  mounted: function(){
      products.forEach(item => {
          this.quantities[item.id]= item.units
      })
  }
};
</script>
