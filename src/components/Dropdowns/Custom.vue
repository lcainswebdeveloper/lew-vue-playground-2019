<template>
  <div class="custom-dropdown-container mx-auto mt-10">
    <div class="p-1">{{ selectedOption.name || 'Please choose an option' }}</div>
    <div v-if="showOptions || true">
      <input v-model="filter" class="search-filter">
      <ul>
        <li :class="{'bg-green text-white': selectedOption.name === option.name}" @click="selectOption(option)" :key="`dropdown-option-${option.id}`" v-for="option in dropdownOptions">
          {{ option.name }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CustomDropdown',
  methods: {
    selectOption(option) {
      this.selectedOption = option;
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
  background:pink;
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
    @apply w-full p-1;
  }
}
</style>
