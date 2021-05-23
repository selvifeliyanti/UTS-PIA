<template>
  <div class="card shadow mt-3">
    <div class="card-body">
      <h5 class="card-title">Create Absen</h5>
      <form class="row g-3" @submit.prevent="store">
        <div class="col-md-6">
          <label for="inputEmail4" class="form-label">ID</label>
          <input
            type="email"
            class="form-control"
            id="inputEmail4"
            v-model="friend.id"
          />
          <div class="alert alert-dager" v-if="validation.id">
            {{ validation.id[0] }}
          </div>
        </div>

        <div class="col-md-6">
          <label for="inputPassword4" class="form-label">Waktu Absen</label>
          <input
            type="password"
            class="form-control"
            id="inputPassword4"
            v-model="friend.waktu_absen"
          />
          <div class="alert alert-dager" v-if="validation.waktu_absen">
            {{ validation.waktu_absen[0] }}
          </div>
        </div>

        <div class="col-md-6">
          <label for="inputPassword4" class="form-label">Id Mahasiswa</label>
          <input
            type="password"
            class="form-control"
            id="inputPassword4"
            v-model="friend.mahasiswa_id"
          />
          <div class="alert alert-dager" v-if="validation.mahasiswa_id">
            {{ validation.mahasiswa_id[0] }}
          </div>
        </div>

        <div class="col-md-6">
          <label for="inputPassword4" class="form-label">Id Matakuliah</label>
          <input
            type="password"
            class="form-control"
            id="inputPassword4"
            v-model="friend.matakuliah_id"
          />
          <div class="alert alert-dager" v-if="validation.matakuliah_id">
            {{ validation.matakuliah_id[0] }}
          </div>
        </div>

        <div class="col-12">
          <label for="inputAddress" class="form-label">Keterangan</label>
          <input
            type="text"
            class="form-control"
            id="inputAddress"
            placeholder="Masukan Keterangan"
            v-model="friend.keterangan"
          />
          <div class="alert alert-dager" v-if="validation.keterangan">
            {{ validation.keterangan[0] }}
          </div>
        </div>

        <div class="col-12">
          <button type="submit" class="btn btn-primary">Tambah</button>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import { reactive, ref } from "vue";
import { useRouter } from "vue-router";
import axios from "axios";
export default {
  setup() {
    const friend = reactive({
      id: "",
      waktu_absen: "",
      mahasiswa_id: "",
      matakuliah_id: "",
      keterangan: "",
    });

    const validation = ref([]);

    const router = useRouter();

    function store() {
      let id = friend.id;
      let waktu_absen = friend.waktu_absen;
      let mahasiswa_id = friend.mahasiswa_id;
      let matakuliah_id = friend.matauliah_id;
      let keterangan = friend.keterangan;

      axios
        .post("http://127.0.0.1:8000/api/friends", {
          id: id,
          waktu_absen: waktu_absen,
          mahasiswa_id: mahasiswa_id,
          matakuliah_id: matakuliah_id,
          keterangan: keterangan,
        })
        .then(() => {
          router.push({
            name: "Home",
          });
        })
        .catch((error) => {
          console.log(error);
        });
    }
    return {
      friend,
      validation,
      router,
      store,
    };
  },
};
</script>
