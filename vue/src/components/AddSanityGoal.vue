<template>
  <form class="box form" v-on:submit.prevent >
    <section>
      <b-field label="ADD SANITY GOAL"> </b-field>

      <b-field label="Name" type="is-primary">
        <b-select
          placeholder="Activity"
          :expanded="true"
          class="activity-input"
          v-model="newGoal.activity"
        >
          <option value="meditiate">Meditate</option>
          <option value="yoga">Yoga</option>
          <option value="go outside">Go Outside</option>
          <option value="breathing exercises">Breathing Exercises</option>
        </b-select>
      </b-field>

      <b-field label="Duration">
        <b-numberinput
         icon-pack="fas"
          class="duration-input"
          v-model="newGoal.duration"
          type="is-primary"
          value="times"
        ></b-numberinput>
      </b-field>

      <b-field label="Select a date">
        <b-datepicker
          :focused-date="date"
          :first-day-of-week="1"
          placeholder="Click to select..."
          v-model="assignDate"
        >
          <b-field>
            <b-autocomplete
              open-on-focus
              readonly
              v-model="month"
              :data="months"
              field="name"
              @select="selectMonth"
            >
            </b-autocomplete>
            <p class="control">
              <span class="button is-static">{{ date.getFullYear() }}</span>
            </p>
          </b-field>
        </b-datepicker>
      </b-field>
      <b-button v-on:click="saveGoal" type="is-primary"
        >{{ this.exisitingGoal ? "Edit" : "Add" }} Sanity Goal</b-button
      >
    </section>
  </form>
</template>

<script>
import goalService from "../services/GoalService.js";
const dateFormat = {
  year: "numeric",
  month: "2-digit",
  day: "2-digit",
};
const locale = "en-US";
export default {
  name: "add-sanity-goal",
  props: ["exisitingGoal"],
  mounted() {
    if (this.exisitingGoal) {
      //target    //source
      Object.assign(this.newGoal, this.exisitingGoal); //enumerates over properties of existing goal and copy onto new goal
    }
  },
  data() {
    return {
      showForm: true,
      newGoal: {
        userGoalsId: "",
        userId: "",
        categoryId: 3,
        category: "sanity",
        activity: "",
        date: new Date().toLocaleDateString(locale, dateFormat),
        perWeek: 0,
        duration: 0,
        complete: false,
      },
      date: new Date(),
      month: null,
      months: [
        { name: "January", value: 0 },
        { name: "February", value: 1 },
        { name: "March", value: 2 },
        { name: "April", value: 3 },
        { name: "May", value: 4 },
        { name: "June", value: 5 },
        { name: "July", value: 6 },
        { name: "August", value: 7 },
        { name: "September", value: 8 },
        { name: "October", value: 9 },
        { name: "November", value: 10 },
        { name: "December", value: 11 },
      ],
    };
  },
  computed: {
    assignDate: {
      get: function () {
        return new Date(this.newGoal.date);
      },
      set: function (dt) {
        this.newGoal.date = dt.toLocaleDateString(locale, dateFormat);
      },
    },
  },
  methods: {
    goalColorChanger() {
      this.$store.commit("CHANGE_COLOR", this.goal);
    },
    selectMonth(option) {
      if (option) {
        this.date = new Date(this.date);
        this.date.setMonth(option.value);
      }
    },
    mounted() {
      this.month = this.months.filter(
        (item) => item.value == this.date.getMonth()
      )[0].name;
    },
    saveGoal() {
      this.newGoal.complete = false;

      if (this.exisitingGoal) {
        goalService
          .update(this.newGoal)
          .then((response) => {
            if (response.status === 200) {
              this.$store.commit("UPDATE_GOAL", this.newGoal);
              this.$store.commit('SET_CURRENT_EDITING_GOAL', null);
            }
          });
      } else {
        goalService.add(this.newGoal).then((response) => {
          if (response.status === 201) {
            this.$store.commit("ADD_NEW", response.data);
            this.$store.commit('SET_CURRENT_EDITING_GOAL', null);
            this.showForm = false;
            this.newGoal = {
              userGoalsId: "",
              userId: "",
              categoryId: 3,
              category: "Sanity",
              activity: "",
              date: new Date().toLocaleDateString(locale, dateFormat),
              perWeek: 0,
              duration: 0,
            };
          }
        });
      }
    },
  },
};
</script>

<style scoped>
.box {
  display: inline-flex;
  align-items: center;
}
</style>