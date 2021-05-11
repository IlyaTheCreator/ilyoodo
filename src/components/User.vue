<template>
  <section>
    <h1 class="distance" v-if="isFemale">
      Горячие милфы радом с тобой
      <span> {{ distance }} км </span>
    </h1>
    <div class="user">
      <div class="wrapper" v-if="isFemale">
        <h1>{{ firstName }} {{ lastName }}</h1>
        <img :src="picture" />
      </div>
      <div v-else class="spinner">
        <a-spin>
          <a-icon
            style="position: relative; left: -40px; font-size: 100px"
            size="large"
            slot="indicator"
            type="loading"
            spin
          />
        </a-spin>
      </div>
      <button @click="update">update</button>
    </div>
  </section>
</template>

<script>
export default {
  name: "User",
  data() {
    return {
      firstName: "",
      lastName: "",
      picture: "",
      phone: "",
      isFemale: false,
      distance: 0,
    };
  },
  methods: {
    update: function () {
      this.fetchUser();
    },
    fetchUser() {
      fetch("https://randomuser.me/api/")
        .then((res) => res.json())
        .then((data) => {
          if (data.results[0].gender === "female") {
            this.distance = Math.ceil(Math.random() * 9);
            this.isFemale = true;
            this.firstName = data.results[0].name.first;
            this.lastName = data.results[0].name.last;
            this.picture = data.results[0].picture.large;
          } else {
            this.isFemale = false;
            setTimeout(() => {
              this.fetchUser();
            }, 500);
          }
        })
        .catch((error) => console.warn(error));
    },
  },
  created() {
    this.fetchUser();
  },
};
</script>

<style>
.distance {
  text-align: center;
  color: #fe4a49;
}

.spinner {
  display: grid;
  place-content: center;
  height: calc(100% - 87.75px);
}

.user {
  position: relative;
  display: flex;
  flex-direction: column;
  width: 350px;
  height: 400px;
  box-shadow: 1px 3px 46px 18px rgba(34, 60, 80, 0.2);
  border-radius: 20px;
  padding-top: 15px;
  margin: 20px auto;
  z-index: 9999;
}

.user h1 {
  text-align: center;
  font-size: 30px;
  font-weight: bold;
  width: 350px;
}

.user .wrapper {
  width: 350px;
  align-self: center;
  display: grid;
  place-content: center;
}

.user img {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  margin: 20px auto;
}

.user .getero {
  height: 277px;
}

.user button {
  width: 180px;
  align-self: center;
  padding: 15px 30px;
  text-transform: uppercase;
  font-weight: bold;
  border: 0;
  border-radius: 15px;
  cursor: pointer;
  background: #fe7171;
  color: #fff;
  transition: all 0.2s ease;
}

.user button:hover {
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
  background: #fe4a49;
  animation-name: name;
}
</style>