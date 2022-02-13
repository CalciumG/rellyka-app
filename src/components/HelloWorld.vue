<template>
  <div>
    <v-row no-gutters>
      <v-col cols="12">
        <v-simple-table>
          <template v-slot:default>
            <thead>
              <tr>
                <th>Player</th>
                <th v-for="item in calResult" :key="item.id" class="text-left">
                  {{ item.id }}
                </th>
              </tr>
            </thead>

            <tbody>
              <tr>
                <td>Cal</td>
                <td
                  class="level"
                  v-for="item in calResult"
                  :key="item.id"
                  ref="level"
                >
                  {{ item.level }}
                </td>
              </tr>
            </tbody>

            <tbody>
              <tr>
                <td>Town</td>
                <td class="level" v-for="item in townResult" :key="item.id">
                  {{ item.level }}
                </td>
              </tr>
            </tbody>

            <tbody>
              <tr>
                <td>Matt</td>
                <td class="level" v-for="item in mattResult" :key="item.id">
                  {{ item.level }}
                </td>
              </tr>
            </tbody>

            <tbody>
              <tr>
                <td>Phil</td>
                <td class="level" v-for="item in philResult" :key="item.id">
                  {{ item.level }}
                </td>
              </tr>
            </tbody>

            <tbody>
              <tr>
                <td>Dan</td>
                <td class="level" v-for="item in djvResult" :key="item.id">
                  {{ item.level }}
                </td>
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
      mattResult: "",
      philResult: "",
      djvResult: "",
      names: ["hosama0", "unholy304"],
      result: {},
      baseUrl:
        "https://rellyka.herokuapp.com/https://secure.runescape.com/m=hiscore_oldschool_seasonal/index_lite.ws?player=",
      skills: [
        "Ovr",
        "Att",
        "Def",
        "St",
        "Hp",
        "Rng",
        "Pray",
        "Mage",
        "Cook",
        "Wc",
        "Fletch",
        "Fish",
        "Fire",
        "Craft",
        "Smith",
        "Mine",
        "Herb",
        "Agi",
        "Thi",
        "Slay",
        "Farm",
        "Rune",
        "Hunt",
        "Const",
      ],
    };
  },

  methods: {
    fetchUser(user, res) {
      res = fetch(this.baseUrl + user)
        .then((response) => response.text())
        .then((data) => (res = data))
        .catch((err) => console.log(err.message));
      return res;
    },

    formatResult(str) {
      var skillCount = 0;
      return str
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

    async getCal(user, res) {
      this.calResult = await this.fetchUser(user, res);
      this.calResult = this.formatResult(this.calResult);
    },

    async getTown(user, res) {
      this.townResult = await this.fetchUser(user, res);
      this.townResult = this.formatResult(this.townResult);
    },

    async getMatt(user, res) {
      this.mattResult = await this.fetchUser(user, res);
      this.mattResult = this.formatResult(this.mattResult);
    },

    async getPhil(user, res) {
      this.philResult = await this.fetchUser(user, res);
      this.philResult = this.formatResult(this.philResult);
    },

    async getVol(user, res) {
      this.djvResult = await this.fetchUser(user, res);
      this.djvResult = this.formatResult(this.djvResult);
    },
  },

  mounted() {
    this.$nextTick(() => {
      console.log(this.$refs.level);
    });
  },

  async created() {
    this.getCal("Hosama0", this.calResult);
    this.getTown("Unholy304", this.townResult);
    this.getMatt("Merlin007100", this.mattResult);
    this.getPhil("Philcold23", this.philResult);
    this.getVol("Dee Jay Vee", this.djvResult);
  },
};
</script>

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

.blue {
  color: red;
}
</style>
