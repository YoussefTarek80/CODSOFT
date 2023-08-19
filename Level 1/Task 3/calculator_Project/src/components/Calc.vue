<template>
  <div class="Box">
    <div class="Result">
      <div class="circles">
        <span></span>
        <span></span>
        <span></span>
      </div>
      <div class="current-operation">
        <span>{{CurrentOp}}</span>
        <span>{{ this.output || 0 }}</span>
        
      </div>
    </div>
    <button @click="clear">AC</button>
    <button @click="change"><i class="fa-solid fa-plus-minus"></i></button>
    <button @click="precent"><i class="fa-solid fa-percent"></i></button>

    <button @click="delnum"><i class="fa-solid fa-delete-left"></i></button>
    <button @click="square"><i class="fa-solid fa-superscript"></i></button>
    <button @click="root">
      <i class="fa-solid fa-square-root-variable"></i>
    </button>
    <button><i class="fa-solid fa-infinity"></i></button>

    <button class="Operators" @click="Proccess('divide')">
      <i class="fa-solid fa-divide"></i>
    </button>

    <button @click="addNumber(7)"><i class="fa-solid fa-7"></i></button>
    <button @click="addNumber(8)"><i class="fa-solid fa-8"></i></button>
    <button @click="addNumber(9)"><i class="fa-solid fa-9"></i></button>

    <button class="Operators" @click="Proccess('multiple')">
      <i class="fa-solid fa-xmark"></i>
    </button>

    <button @click="addNumber(4)"><i class="fa-solid fa-4"></i></button>
    <button @click="addNumber(5)"><i class="fa-solid fa-5"></i></button>
    <button @click="addNumber(6)"><i class="fa-solid fa-6"></i></button>

    <button class="Operators" @click="Proccess('mince')">
      <i class="fa-solid fa-minus"></i>
    </button>

    <button @click="addNumber(1)"><i class="fa-solid fa-1"></i></button>
    <button @click="addNumber(2)"><i class="fa-solid fa-2"></i></button>
    <button @click="addNumber(3)"><i class="fa-solid fa-3"></i></button>

    <button class="Operators" @click="Proccess('add')" >
      <i class="fa-solid fa-plus"></i>
    </button>

    <button class="end-Row" @click="addNumber(0)">
      <i class="fa-solid fa-0"></i>
    </button>
    <button @click="Dot">.</button>
    <button class="Operators" @click="equalClick">
      <i class="fa-solid fa-equals"></i>
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      output: "",
      lastValue: null,
      operationDone: false,
      CurrentOp:''
    };
  },
  methods: {
    clear() {
      this.output = "";
      this.operationDone = false;
      this.CurrentOp='';
    },
    change() {
      if (this.output != "-") {
        this.output = -Math.abs(this.output);
      }
    },
    delnum() {
      if (this.output == "") {
        return false;
      } else {
        this.output = parseInt(this.output / 10);
        this.CurrentOp='';
      }
    },
    precent() {
      if (this.output == "") {
        this.output = "";
      } else {
        this.output = parseFloat(this.output) / 100;
        this.CurrentOp='';
      }
    },
    root() {
      if (this.output == "") {
        this.output = "";
      } else {
        this.output = Math.sqrt(this.output);
        this.CurrentOp='';
      }
    },
    square() {
      if (this.output == "") {
        this.output = "";
      } else {
        this.output = Math.pow(this.output, 2);
        this.CurrentOp='';
      }
    },
    addNumber(num) {
      if (this.operationDone) {
        this.output = "";
        this.operationDone = false;
      }
      this.output = `${this.output}${num}`;
    },
    Dot() {
      if (this.output.indexOf(".") === -1) {
        this.output = this.output + ".";
      }
    },
    Proccess(operation) {
      if (operation == "add") {
        if (this.output == "") {
          this.op = (a, b) => {
            return parseFloat(0) + parseFloat(b);
          };
        } else {
          this.CurrentOp='+';
          this.op = (a, b) => {
            return parseFloat(a) + parseFloat(b);
          };
        }
      } else if (operation == "mince") {
        if (this.output == "") {
          this.op = (a, b) => {
            return parseFloat(0) - parseFloat(b);
          };
        } else {
          this.CurrentOp='-';
          this.op = (a, b) => {
            return parseFloat(a) - parseFloat(b);
          };
        }
      } else if (operation == "multiple") {
        if (this.output == "") {
          this.op = (a, b) => {
            return parseFloat(0) * parseFloat(b);
          };
        } else {
          this.CurrentOp='*';
          this.op = (a, b) => {
            return parseFloat(a) * parseFloat(b);
          };
        }
      } else if (operation == "divide") {
        if (this.output == "") {
          this.op = (a, b) => {
            return parseFloat(0) / parseFloat(b);
          };
        } else {
          this.CurrentOp='/';
          this.op = (a, b) => {
            return parseFloat(a) / parseFloat(b);
          };
        }
      }
      this.lastValue = this.output;
      this.operationDone = true;
    },
    equalClick() {
      if (this.output == "" || this.lastValue == null) {
        return false;
      } else {
        this.output = `${this.op(
          parseFloat(this.lastValue),
          parseFloat(this.output)
        )}`;
        this.lastValue = null;
        this.CurrentOp='';
      }
    },
  },
};
</script>
<style scoped>
@import "./style.css";
</style>
