<template>
  <div v-click-outside="reset" class="custom-dropdown-container mx-auto mt-10 p-4">
    <div class="p-1" @click="showOptions = true">{{ selectedOption.name || 'Please choose an option' }}</div>
    <div v-if="showOptions">
      <input
        @keydown.down="selectNext()"
        @keydown.up="selectPrevious()"
        @keydown.enter.prevent="selectOptionFromInput()"
        @keydown.tab.prevent="selectNext"
        v-model="filter"
        class="search-filter">
      <ul>
        <li :class="optionColours(option, i)" @click="selectOption(option)" :key="`dropdown-option-${option.id}`" v-for="(option, i) in filteredOptions">
          {{ option.name }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import ClickOutside from 'vue-click-outside';

export default {
  name: 'CustomDropdown',
  computed: {
    filteredOptions() {
      return this.dropdownOptions.filter(o => {
        if (this.filter === '') return true;
        return o.name.toLowerCase().indexOf(this.filter.toLowerCase()) !== -1;
      });
    },
  },
  directives: {
    ClickOutside,
  },
  methods: {
    selectOptionFromInput() {
      const check = this.filteredOptions[(this.tabIndex - 1)];
      if (check) {
        this.selectOption(this.filteredOptions[(this.tabIndex - 1)]);
      }
    },
    optionColours(option, key) {
      console.log(`(key ${key} === (this.tabIndex (${this.tabIndex - 1})) && this.tabIndex !== 0)`);
      return {
        'bg-green text-white': this.selectedOption.name === option.name,
        'bg-grey text-white': (key === (this.tabIndex - 1) && this.tabIndex !== 0),
      };
    },
    selectNext() {
      if (this.tabIndex < this.filteredOptions.length) {
        this.tabIndex += 1;
      } else {
        this.tabIndex = 1;
      }
    },
    selectPrevious() {
      if (this.tabIndex > 1) {
        this.tabIndex -= 1;
      } else {
        this.tabIndex = this.filteredOptions.length;
      }
    },
    reset() {
      // this.selectedOption = {};
      this.filter = '';
      this.showOptions = false;
      this.tabIndex = 0;
    },
    selectOption(option) {
      this.selectedOption = option;
      this.reset();
    },
  },
  data() {
    return {
      tabIndex: 0,
      filter: '',
      selectedOption: {},
      showOptions: false,
      dropdownOptions: [
        {
          id: 1,
          name: 'Lewis Cains',
        },
        {
          id: 2,
          name: 'Ian Botham',
        },
        {
          id: 3,
          name: 'Donald Duck',
        },
      ],
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.custom-dropdown-container{
  max-width:400px;
  border: 1px solid #ccc;
  color: #212121;
  ul{
    list-style-type:none;
    margin:0;
    li{
      transition: all 0.3s ease;
      @apply p-1;
      &:hover{
        cursor:pointer;
        background-color: #ccc;
      }
    }
  }
  .search-filter{
    width: 97%;
    @apply my-1 p-1;
  }
}
</style>
