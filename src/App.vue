<template>
  <div
    class="d-flex aligns-items-center justify-content-center"
    style="height: 100%"
  >
    <div class="main my-auto" style="min-width: 300px !important">
      <h1 class="pass mb-4">{{ pass }}</h1>
      <MDBRow style="width: 350px" class="mx-auto">
        <MDBCol col="4"> </MDBCol>
        <MDBCol col="4">
          <MDBBtn v-on:click="generar()" color="dark">Generate</MDBBtn>
        </MDBCol>
        <MDBCol col="4" align="left">
          <MDBBtn v-on:click="copiar()" floating color="dark"><i class="far fa-clone"></i></MDBBtn>
        </MDBCol>
      </MDBRow>

      <div class="options mt-5 mx-auto" style="width: 300px">
        <div class="mx-auto" style="width: 40%">
          <MDBSwitch v-model="useSymbols" label="Symbols" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref, watch } from "vue";
import { MDBBtn, MDBSwitch, MDBCol, MDBRow } from "mdb-vue-ui-kit";

const pass = ref(null);

const useSymbols = ref(false);

pass.value = 5;

const generar = () => {
  const dictionary = !useSymbols.value
    ? "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz"
    : "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz~!@-_#$";

  let newpass = Array(14).fill(0);

  newpass = newpass.map(() => {
    return dictionary[Math.floor(Math.random() * dictionary.length)];
  });

  pass.value = newpass.join("");
};

const copiar = () => {
  navigator.clipboard.writeText(pass.value);

}

watch([useSymbols], () => {
  generar();
});

onMounted(() => {
  generar();
});
</script>

<style>
#app {
  font-family: Roboto, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #1f2c39;
}


</style>
