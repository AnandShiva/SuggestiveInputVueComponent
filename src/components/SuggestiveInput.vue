<template>
  <div>
    <div class="suggestiveInput">
      <input type="text" v-model="currentUserInput" />
      <ul v-show="showPopUp" class="popup"> 
        <li class="list_item"
          @click="suggestionItemSelected(item)"
          v-bind:key="index+200"
          v-html="highLightMatchingSection(currentUserInput, item)"
          v-for="(item,index) in matchingSuggestionItems"
        ></li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
input {
  padding: 10px;
  display: block;
  background-color: inherit;
}
ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

.popup {
  position: absolute;
  visibility: hidden;
  width: 100%;
}
.popup.show {
  visibility: visible;
  cursor: pointer;
  background-color: #ffffff ;
  z-index: 10;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.suggestiveInput {
  position: relative;
  width: fit-content;
}

.list_item{
  padding-left: 1em;
}

.list_item:hover{
  background-color: #d6d6d6;
  text-align: start;
  border : solid;
  border-width: 3px;
  border-color: #d6d6d600;
}
</style>

<script>
export default {
  data() {
    return {
      showPopUp: false,
      currentUserInput: ""
    };
  },
  props: ["suggestionProps"],
  watch: {
    currentUserInput: function() {
      let currentInput = this.currentUserInput;
      let popup = this.$el.getElementsByTagName("ul")[0];
      if (this.showPopUp) {
        popup.classList.add("show");
      } else {
        popup.classList.remove("show");
      }
    }
  },
  computed: {
    matchingSuggestionItems: function() {
      this.showPopUp = true;
      let currentInput = this.currentUserInput.toLowerCase();
      let suggestedItems = this.$props.suggestionProps.filter(items => {
        return items.toLowerCase().indexOf(currentInput) != -1;
      });
      return suggestedItems;
    },
  },
  methods: {
    suggestionItemSelected(itemText) {
      this.currentUserInput = itemText;
      this.showPopUp = false;
    },
    highLightMatchingSection(currentUserInput, suggestedItem){
      let matchingSectionIndex =-1;
      if(currentUserInput != ""){
        matchingSectionIndex = suggestedItem.toLowerCase().indexOf(currentUserInput.toLowerCase());
      }
      if(matchingSectionIndex == -1){
        return suggestedItem;
      }
      let highlightedHtmlString = "";
      highlightedHtmlString = suggestedItem.substring(0,matchingSectionIndex);
      highlightedHtmlString += "<b>";
      highlightedHtmlString += suggestedItem.substring(matchingSectionIndex,matchingSectionIndex+currentUserInput.length) + "</b>";
      highlightedHtmlString += suggestedItem.substring(matchingSectionIndex+currentUserInput.length);
      return highlightedHtmlString;
      
    }
  }
};
</script>