<template>
  <div>
    <v-row no-gutters>
      <v-col cols="2">
        <v-simple-table>
          <template v-slot:default>
            <thead>
              Cal
              <tr>
                <th class="text-left">Skill</th>
                <th class="text-left">Level</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in calResult" :key="item.id">
                <td>{{ item.id }}</td>
                <td>{{ item.level }}</td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-col>

      <v-col cols="2">
        <v-simple-table>
          <template v-slot:default>
            <thead>
              Town
              <tr>
                <th class="text-left">Skill</th>
                <th class="text-left">Level</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in townResult" :key="item.id">
                <td>{{ item.id }}</td>
                <td>{{ item.level }}</td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  data() {
    return {
      calResult: "",
      townResult: "",
      names: ["hosama0", "unholy304"],
      result: {},
      skills: [
        "Overall",
        "Attack",
        "Defence",
        "Strength",
        "Hitpoints",
        "Ranged",
        "Prayer",
        "Magic",
        "Cooking",
        "Woodcutting",
        "Fletching",
        "Fishing",
        "Firemaking",
        "Crafting",
        "Smithing",
        "Mining",
        "Herblore",
        "Agility",
        "Thieving",
        "Slayer",
        "Farming",
        "Runecrafting",
        "Hunter",
        "Construction",
      ],
    };
  },

  methods: {
    async getCal() {
      var skillCount = 0;
      await this.fetchCal();

      this.calResult = this.calResult
        .replace(/\n/g, " ")
        .split(" ")
        .map((str) => ({
          rank: str.split(",")[0],
          level: str.split(",")[1],
          exp: str.split(",")[2],
          id: this.skills[skillCount++],
        }))
        .slice(0, 24);
    },

    fetchCal() {
      var result = fetch(
        "https://rellyka.herokuapp.com/https://secure.runescape.com/m=hiscore_oldschool_seasonal/index_lite.ws?player=hosama0"
      )
        .then((response) => response.text())
        .then((data) => (this.calResult = data))
        .catch((err) => console.log(err.message));
      return result;
    },

    async getTown() {
      var skillCount = 0;
      await this.fetchTown();

      this.townResult = this.townResult
        .replace(/\n/g, " ")
        .split(" ")
        .map((str) => ({
          rank: str.split(",")[0],
          level: str.split(",")[1],
          exp: str.split(",")[2],
          id: this.skills[skillCount++],
        }))
        .slice(0, 24);
    },

    fetchTown() {
      var result = fetch(
        "https://rellyka.herokuapp.com/https://secure.runescape.com/m=hiscore_oldschool_seasonal/index_lite.ws?player=unholy304"
      )
        .then((response) => response.text())
        .then((data) => (this.townResult = data))
        .catch((err) => console.log(err.message));
      return result;
    },
  },

  async mounted() {
    this.getCal();
    this.getTown();
  },
};
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
