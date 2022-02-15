<template>
  <div>
    <div v-for="item in resultArray" :key="item.name">
      <h1>{{ item.name }}</h1>

      <div v-for="object in item" :key="object.id">
        <div v-for="skill in object" :key="skill.id">
          <h5 id="skill">{{ skill.id }} {{ skill.level }}</h5>
        </div>
      </div>
    </div>
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
      resultArray: [],
      names: [
        "hosama0",
        "unholy304",
        "Merlin007100",
        "Philcold23",
        "Dee Jay Vee",
      ],
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
    fetchUser(user) {
      return fetch(this.baseUrl + user)
        .then((response) => response.text())
        .then((data) => (this.arrayResult = data))
        .catch((err) => console.log(err.message));
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

    async getUser(user) {
      let result = await this.fetchUser(user);
      result = this.formatResult(result);
      let final = {
        name: user,
        props: result,
      };
      return final;
    },

    getData() {
      this.names.forEach((name) => {
        this.resultArray.push(this.getUser(name));
      });
      return this.resultArray;
    },
  },

  created() {
    this.getData();

    Promise.all(this.resultArray).then((values) => {
      this.resultArray = values;
    });
  },

  mounted() {},
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
