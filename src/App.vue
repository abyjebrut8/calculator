<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-md-12">
        <input
          class="form-control m-input"
          v-model="inputSatu"
          type="text"
          @keydown.exact="onlyNumeric"
          @input="handleInput"
          Size="35"
          :maxlength="4"
        />
        &nbsp;
        <input
          type="checkbox"
          id="cInputSatu"
          value="1"
          v-model="checkSatu"
          @click="handleClickCheckBox(1)"
        />
      </div>
      <div class="col-md-12" style="padding-top: 10px">
        <input
          type="text"
          v-model="inputDua"
          @keydown.exact="onlyNumeric"
          @input="handleInput"
          Size="35"
          :maxlength="4"
        />&nbsp;
        <input
          type="checkbox"
          id="cInputDua"
          value="2"
          v-model="checkDua"
          @click="handleClickCheckBox(2)"
        />
      </div>
      <div class="col-md-12" style="padding-top: 10px">
        <input
          type="text"
          v-model="inputTiga"
          @keydown.exact="onlyNumeric"
          @input="handleInput"
          Size="35"
          :maxlength="4"
        />&nbsp;
        <input
          type="checkbox"
          id="cInputTiga"
          value="2"
          v-model="checkTiga"
          @click="handleClickCheckBox(3)"
        />
      </div>
      <div class="col-md-12" style="padding-top: 10px">
        <button class="button" :type="button" @click="handleClickButton('+')">
          +
        </button>
        <button class="button" :type="button" @click="handleClickButton('-')">
          -
        </button>
        <button class="button" :type="button" @click="handleClickButton('x')">
          x
        </button>
        <button class="button" :type="button" @click="handleClickButton('/')">
          /
        </button>
      </div>
      <div class="col-md-12" style="padding-top: 10px">
        <hr />
        <span
          ><b>Hasil : {{ hasil }}</b></span
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputSatu: 0,
      inputDua: 0,
      inputTiga: 0,
      checkSatu: false,
      checkDua: false,
      checkTiga: false,
      checkedTotal: 0,
      hasil: 0,
    };
  },

  methods: {
    handleInput(event) {
      if (event.target.value.length > parseInt(this.maxlength)) {
        event.target.value = this.value.slice(0, this.maxLength);
      }
      this.$emit("input", event.target.value);
    },

    handleClickButton(val) {
      if (parseInt(this.checkedTotal) < 2) {
        alert("Data Harus lebih dari 1");
      } else {
        var nilai1 = 0;
        var nilai2 = 0;
        var nilai3 = 0;
        if (this.checkSatu) {
          nilai1 = this.inputSatu;
        }
        if (this.checkDua) {
          nilai2 = this.inputDua;
        }
        if (this.checkTiga) {
          nilai3 = this.inputTiga;
        }

        if (val == "+") {
          this.hasil = parseInt(nilai1) + parseInt(nilai2) + parseInt(nilai3);
        } else if (val == "-") {
          if (nilai1 > 0 && nilai2 > 0 && nilai3 > 0) {
            this.hasil = parseInt(nilai1) - parseInt(nilai2) - parseInt(nilai3);
          } else if (nilai1 > 0 && nilai2 > 0 && nilai3 <= 0) {
            this.hasil = parseInt(nilai1) - parseInt(nilai2);
          } else if (nilai1 > 0 && nilai2 <= 0 && nilai3 > 0) {
            this.hasil = parseInt(nilai1) - parseInt(nilai3);
          } else if (nilai1 <= 0 && nilai2 > 0 && nilai3 > 0) {
            this.hasil = parseInt(nilai2) - parseInt(nilai3);
          }
        } else if (val == "x") {
          if (nilai1 > 0 && nilai2 > 0 && nilai3 > 0) {
            this.hasil = parseInt(nilai1) * parseInt(nilai2) * parseInt(nilai3);
          } else if (nilai1 > 0 && nilai2 > 0 && nilai3 <= 0) {
            this.hasil = parseInt(nilai1) * parseInt(nilai2);
          } else if (nilai1 > 0 && nilai2 <= 0 && nilai3 > 0) {
            this.hasil = parseInt(nilai1) * parseInt(nilai3);
          } else if (nilai1 <= 0 && nilai2 > 0 && nilai3 > 0) {
            this.hasil = parseInt(nilai2) * parseInt(nilai3);
          }
        } else if (val == "/") {
          if (nilai1 > 0 && nilai2 > 0 && nilai3 > 0) {
            this.hasil = parseInt(nilai1) / parseInt(nilai2) / parseInt(nilai3);
          } else if (nilai1 > 0 && nilai2 > 0 && nilai3 <= 0) {
            this.hasil = parseInt(nilai1) / parseInt(nilai2);
          } else if (nilai1 > 0 && nilai2 <= 0 && nilai3 > 0) {
            this.hasil = parseInt(nilai1) / parseInt(nilai3);
          } else if (nilai1 <= 0 && nilai2 > 0 && nilai3 > 0) {
            this.hasil = parseInt(nilai2) / parseInt(nilai3);
          }
        }
      }
    },

    handleClickCheckBox(val) {
      var nilai = parseInt(this.checkedTotal);
      if (val == 1) {
        if (this.checkSatu == false) {
          this.checkedTotal = nilai + 1;
          this.checkSatu = true;
        } else {
          this.checkedTotal = nilai - 1;
          this.checkSatu = false;
        }
      } else if (val == 2) {
        if (this.checkDua == false) {
          this.checkedTotal = nilai + 1;
          this.checkDua = true;
        } else {
          this.checkedTotal = nilai - 1;
          this.checkDua = false;
        }
      } else if (val == 3) {
        if (this.checkTiga == false) {
          this.checkedTotal = nilai + 1;
          this.checkTiga = true;
        } else {
          this.checkedTotal = nilai - 1;
          this.checkTiga = false;
        }
      }
    },

    onlyNumeric(event) {
      var charCode = event.which ? event.which : event.keyCode;
      if (
        charCode > 31 &&
        (charCode < 48 || charCode > 57) &&
        charCode !== 46
      ) {
        event.preventDefault();
      } else {
        return true;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.button {
  border-radius: 4px;
  background-color: #4caf50; /* Green */
  border: none;
  color: white;
  padding: 15px 25px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}
input[type="text"] {
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: none;
  background-color: #63e0b2;
  color: rgb(17, 6, 6);
  font-size: 14px;
}
</style>
