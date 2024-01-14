<script>
export default  {
  data() {
    return {
      firstName: 'John',
      lastName: 'Doe',
      email: 'john@gmail.com',
      gender: 'male',
      picture: 'https://randomuser.me/api/potraits/men/10.jpg',
    }
  },
  methods: {
    async getUser() {
      const response = await fetch('https://randomuser.me/api');

      const { results } = await response.json();

      this.firstName = results[0].name.first
      this.lastName = results[0].name.last
      this.email = results[0].email
      this.gender = results[0].gender
      this.picture = results[0].picture.large
    }
  }
}
</script>

<template>
  <img v-bind:class="gender" v-bind:src="picture">
  <h1 class="mb-4 font-normal">{{firstName}} {{lastName}}</h1>
  <h3 class="mb-4 font-normal">Email : {{email}}</h3>
  <button v-on:click="getUser()" class="focus:outline-none hover:scale-95 cursor-pointer inline-block bg-indigo-400 text-white text-xl py-4 px-6 rounded-2xl">Get Random User</button>
</template>

<style scoped>
  img {
    @apply rounded-[50%] border-4 border-solid mb-4;

    &.male {
      @apply border-cyan-300 bg-cyan-300;
    }
    &.female {
      @apply border-pink-500 bg-pink-500 text-gray-200;
    }
  }
</style>

