<template>
  <div id="main">
    <h1>Welcome to MusicScape</h1>  
    <h4>Feel free to search for music and take a listen</h4>
    <h4>You can also Login or register to create an account</h4>   
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      playLists: {},
    }
  },
  methods: {
    getPlaylist() {
      var vm = this
      let yesterday =
        new Date().getFullYear() +
        '-' +
        ('0' + (new Date().getMonth() + 1)).slice(-2) +
        '-' +
        ('0' + (new Date().getDate() - 1)).slice(-2)

      let today =
        new Date().getFullYear() +
        '-' +
        ('0' + (new Date().getMonth() + 1)).slice(-2) +
        '-' +
        ('0' + new Date().getDate()).slice(-2)

      if (today[9] == 1 && today[8] == 0) {
        yesterday =
          new Date().getFullYear() +
          '-' +
          ('0' + new Date().getMonth()).slice(-2) +
          '-' +
          30
      }

      // if (yesterday[8] && yesterday[9] == 0) {
      //   yesterday[8] = 3
      // }

      let url =
        'https://api.jamendo.com/v3.0/playlists/?client_id=a31f0360&format=jsonpretty&datebetween=' +
        yesterday +
        '_' +
        today

      axios
        .get(url)
        .then(function (response) {
          // handle success
          console.log(response)
          vm.playLists = response.data.results
          console.log(JSON.stringify(vm.playLists))
        })
        .catch(function (error) {
          // handle error
          console.log(error)
        })
    },

    goToPlayList() {
      let url = axios
        .get(url)
        .then(function (response) {
          // handle success
          console.log(response.data)
        })
        .catch(function (error) {
          // handle error
          console.log(error)
        })
    },
  },
  mounted() {
    this.getPlaylist()
  },
}
</script>

<style>
.list {
  list-style: none;

  margin-top: 1rem;
  display: flex;
  justify-content: center;
}

@media only screen and (max-width: 770px) {


  b-card {
    margin-top: 2rem;
  }

  h1 {
    font-size: 1.5rem;
  }
}



h1, h4 {
  color: white;
}
</style>
