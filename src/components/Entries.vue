<template>
  <div>
    <button id="toggleButton" @click="sortedEntries">{{ (newToOld) ? "Newest to oldest" : "Oldest to newest" }}</button>
    <div class="entry" v-for="(entry, index) in entries" :key="index">
      <h3>{{entry.title}}</h3>
      <div>{{entry.date | formatDate}}</div>
      <img :src="entry.image"/>
      <div>{{entry.text}}</div>
    </div>
  </div>
</template>

<script>
    export default {
      name: 'Entries',
      props: {
        entries: Array
      },
      data: function () {
        return {
          newToOld: true
        }
      },
      computed: {
        sortedEntries: function () {
          let entries = this.entries
          if (this.newToOld) {
            entries.sort((a, b) => (a.date < b.date) ? 1 : -1)
          } else {
            entries.sort((a, b) => (a.date < b.date) ? -1 : 1)
          }
          return entries
        }
      },
      methods: {
        toggleList: function () {
          this.newToOld = !(this.newToOld)
          this.sortedEntries
        }
      },
      filters: {
        formatDate: function (value) {
          if (!value) return ''
          let date = new Date(value);
          let months = [
              "January",
              "February",
              "March",
              "April",
              "May",
              "June",
              "July",
              "August",
              "September",
              "October",
              "November",
              "December"
          ];
          let days= ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]
          let timeOfDay = (date.getHours() > 12) ? "PM" : "AM";
          return days[date.getDay()] + ", "
              + months[date.getMonth() + 1] + " "
              + date.getDate() + ", "
              + date.getFullYear() + " "
              + date.getHours() + ":"
              + date.getMinutes() + " "
              + timeOfDay
        }
      }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
