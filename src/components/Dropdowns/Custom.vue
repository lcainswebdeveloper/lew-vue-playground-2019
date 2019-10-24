<template>
  <div v-click-outside="reset" class="custom-dropdown-container mx-auto mt-10 p-4">
    <div class="p-1" @click="showOptions = true">{{ selectedOption.name || 'Please choose an option' }}</div>
    <div v-if="showOptions">
      <input v-model="filter" class="search-filter">
      <ul>
        <li :class="{'bg-green text-white': selectedOption.name === option.name}" @click="selectOption(option)" :key="`dropdown-option-${option.id}`" v-for="option in filteredOptions">
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
    reset() {
      // this.selectedOption = {};
      this.filter = '';
      this.showOptions = false;
    },
    selectOption(option) {
      this.selectedOption = option;
      this.reset();
    },
  },
  data() {
    return {
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
