<template>
  <div class="home">
    <!--<img alt="Vue logo" src="../assets/logo.png">-->
    <Slider />
    <hr class="my-3">
    <router-link class="btn btn-primary" to="/createfriends">Tambah</router-link>
    <table class="table">
  <thead>
    <tr>
      <th scope="col">ID</th>
      <th scope="col">Waktu Absen</th>
      <th scope="col">ID Mahasiswa</th>
      <th scope="col">ID Matakuliah</th>
      <th scope="col">Kehadiran</th>
      <th scope="col">Aksi</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(friends, index) in friends" :key="index">
      <td>{{ friends.id}}</td>
      <td>{{ friends.waktu_absen}}</td>
      <td>{{ friends.mahasiswa_id}}</td>
      <td>{{ friends.matakuliah_id}}</td>
      <td>{{ friends.keterangan}}</td>
      <td>
        <router-link class="btn btn-success" to="/editfriend">Edit</router-link>
        <button class="btn btn-danger">Delete</button>
      </td>
    </tr>
  </tbody>
</table>
  </div>
</template>

<script>
import axios from 'axios'
// @ is an alias to /src
import Slider from '@/components/Slider.vue'
import { onMounted, ref } from 'vue'

export default {
  name: 'Home',
  components: {
    Slider
  },
  setup(){
    let friends = ref([])
    onMounted(() => {
      axios.get('http://127.0.0.1:8000/api/friends')
      .then(response => {
        friends.value = response.data.data
    })
    .catch(error =>{
      console.log(error)
    })
    })
    return {
      friends
    }
  }
};
</script>
