<template>
  <v-container>
    <v-row class="text-left justify-start">
      <v-col class="col-4">
        <v-select
          v-model="gender"
          :items="genderList"
          label="Choose gender"
          @change="showInfo"
          clearable
        >
        </v-select>
      </v-col>
    </v-row>
    <v-row class="text-left justify-end">
      <v-col class="col-4">
        <v-avatar class="profile-image" v-if="imageSrc" size="100">
          <img :src="imageSrc" alt="Profile Image" />
        </v-avatar>
        <div v-if="firstName || lastName">
          <p class="name-line">{{ firstName }}</p>
          <v-divider class="col-4"></v-divider>
          <p class="name-line">{{ lastName }}</p>
          <v-divider class="col-4"></v-divider>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Vue from "vue";
export default {
  name: "RecrutationApp",

  data: () => ({
    gender: null,
    genderList: ["female", "male"],
    firstName: "",
    lastName: "",
    imageSrc: ""
  }),
  methods: {
    getData(genderType) {
      const api = "https://randomuser.me/api/?gender";
      return Vue.axios.get(`${api}=${genderType}`);
    },
    async showInfo(gender) {
      if (this.gender) {
        try {
          const data = await this.getData(gender);
          if (data.status !== 200) {
            throw new Error();
          }
          const personInfo = data.data.results[0];
          this.firstName =
            personInfo && personInfo.name && personInfo.name.first;
          this.lastName = personInfo && personInfo.name && personInfo.name.last;
          this.imageSrc =
            personInfo && personInfo.picture
              ? personInfo.picture.medium || personInfo.picture.thumbnail
              : null;
        } catch (e) {
          console.log("error on catch");
        }
      }
    }
  }
};
</script>
<style lang="scss" scoped>
.container {
  margin-top: 10%;
}
.profile-image {
  margin-bottom: 20px;
}
</style>
