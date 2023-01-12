<template>
  <v-container>
    <v-row>
      <v-col cols="4">
        <v-select
          v-model="selectedProgram"
          :items="programs"
          label="Программа:"
          item-text="name"
          item-value="id"
          dense
        ></v-select></v-col
      ><v-col cols="4">
        <v-text-field
        class="inputSumm"
          v-model="summ"
          label="Сумма займа:"
          type="number"
          dense
        ></v-text-field></v-col
      ><v-col cols="4">
        <v-label>Ежемес. платеж:</v-label>
        <v-slider
          v-model="monthlyPay"
          track-color="grey"
          color="green"
          always-dirty
          min="10000"
          :max="summ"
          step="10000"
          dense
        >
          <template v-slot:prepend>
            <v-icon @click="decrement"> mdi-minus </v-icon>
          </template>

          <template v-slot:append>
            <v-icon @click="increment"> mdi-plus </v-icon>
          </template>
        </v-slider>
      </v-col>
    </v-row>
    <table class="tg">
      <thead>
        <tr>
          <th class="tg-header">Вид займа</th>
          <th class="tg-header" v-for="loan in loans" :key="loan.id">
            {{ loan.name }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td class="tg-merge" colspan="6">Общие сведения</td>
        </tr>
        <tr>
          <td class="tg-field">Договорная сумма</td>
          <th class="tg" v-for="loan in loans" :key="loan.id">
            {{ loan.contractSum }}
          </th>
        </tr>
        <tr>
          <td class="tg-field">сумма</td>
          <td class="tg">{{ new Intl.NumberFormat().format(summ) }} т</td>
          <td class="tg">{{ new Intl.NumberFormat().format(summ) }} т</td>
          <td class="tg">{{ new Intl.NumberFormat().format(summ) }} т</td>
          <td class="tg">{{ new Intl.NumberFormat().format(summ) }} т</td>
          <td class="tg">{{ new Intl.NumberFormat().format(summ) }} т</td>
        </tr>
        <tr>
          <td class="tg-field">общий</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-field">Ежемеся</td>
          <td class="tg">{{ monthlyPay }}</td>
          <td class="tg">{{ monthlyPay }}</td>
          <td class="tg">{{ monthlyPay }}</td>
          <td class="tg">{{ monthlyPay }}</td>
          <td class="tg">{{ monthlyPay }}</td>
        </tr>
        <tr>
          <td class="tg-field">переплата</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-merge" colspan="6">Начальные</td>
        </tr>
        <tr>
          <td class="tg-field">ЧСД</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-field">Срок без</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-field">Ежемеся</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-field">Переход</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-field">Ставка</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-field">Метод</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-merge" colspan="6">Жилищный</td>
        </tr>
        <tr>
          <td class="tg-field">Срок жилищ</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-field">Ежемесячный</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-field">Ставка</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-field">Метод</td>
          <td class="tg">Аннуетет</td>
          <td class="tg">Аннуетет</td>
          <td class="tg">Аннуетет</td>
          <td class="tg">Аннуетет</td>
          <td class="tg">Аннуетет</td>
        </tr>
        <tr>
          <td class="tg-merge" colspan="6">Дополнительно</td>
        </tr>
        <tr>
          <td class="tg-field">Необходимо</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-field">Ориентировочные</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-footer"></td>
          <td class="tg-footer">
            <v-btn color="primary" @click="sendToParent"
              ><v-icon left>mdi-check-circle-outline</v-icon> Выбрать</v-btn
            >
          </td>
          <td class="tg-footer">
            <v-btn color="primary"
              ><v-icon left>mdi-check-circle-outline</v-icon> Выбрать</v-btn
            >
          </td>
          <td class="tg-footer">
            <v-btn color="primary"
              ><v-icon left>mdi-check-circle-outline</v-icon> Выбрать</v-btn
            >
          </td>
          <td class="tg-footer">
            <v-btn color="orange" disabled
              ><v-icon left dark>mdi-close-circle-outline</v-icon> Не
              доступен</v-btn
            >
          </td>
          <td class="tg-footer">
            <v-btn color="orange" disabled
              ><v-icon left dark>mdi-close-circle-outline</v-icon> Не
              доступен</v-btn
            >
          </td>
        </tr>
      </tbody>
    </table>
  </v-container>
</template>
<script>
export default {
  name: "TransposeTable",
  mounted() {
    console.log("Starting connection to WebSocket Server");
    this.connection = new WebSocket("ws://localhost:8081");
    window.top.postMessage("GetSumm", "*");
    var scope = this;
    window.onmessage = function (e) {
      // inside the iframe
      if (e.data?.summ) {
        console.log("child", e);
        //alert("It childs works!");

        console.log("summ recived", e.data.summ);
        scope.summ = e.data.summ;
        console.log("scope.summ", scope.summ);
      }
    };
    console.log("data", this);
  },
  data() {
    return {
      connection: null,
      summ: 20500000,
      monthlyPay: 5000000,
      selectedProgram: "Втричное жилье",
      programs: ["Втричное жилье"],
      fields: [
        { id: 11, name: "test fields 11" },
        { id: 12, name: "test fields 12" },
        { id: 13, name: "test fields 13" },
        { id: 14, name: "test fields 14" },
        { id: 15, name: "test fields 15" },
        { id: 16, name: "test fields 16" },
        { id: 17, name: "test fields 17" },
        { id: 18, name: "test fields 18" },
      ],
      loans: [
        {
          id: 1,
          name: 'Пром. жилищный заем "Жекіл"',
          contractSum: "2050000.00 т",
        },
        {
          id: 2,
          name: 'Пром. жилищный заем "Жекіл-2"',
          contractSum: "2050000.00 т",
        },
        {
          id: 3,
          name: "Промежуточный жилищный заем",
          contractSum: "2050000.00 т",
        },
        { id: 4, name: "Предварительный жилищный заем", contractSum: "0.00 т" },
        { id: 5, name: "Жилищный заем", contractSum: "2050000.00 т" },
      ],
    };
  },
  methods: {
    decrement() {
      this.monthlyPay = this.monthlyPay - 10000;
    },
    increment() {
      this.monthlyPay = this.monthlyPay + 10000;
    },
    sendToParent() {
      window.top.postMessage("hello world2", "*");
    },
  },
};
</script>
<style scoped>
.inputSumm >>> input[type="number"] {
  -moz-appearance: textfield;
}
.inputSumm >>> input::-webkit-outer-spin-button,
.inputSumm >>> input::-webkit-inner-spin-button {
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}
.tg {
  border-collapse: collapse;
  border-color: #9abad9;
  border-spacing: 0;
}
.tg td {
  background-color: #ffffff;
  border-color: #9abad9;
  border-style: solid;
  border-width: 1px;
  color: #444;
  font-family: Arial, sans-serif;
  font-size: 14px;
  overflow: hidden;
  padding: 5px 5px;
  word-break: normal;
  text-align: center;
}
.tg th {
  background-color: #ffffff;
  border-color: #9abad9;
  border-style: solid;
  border-width: 1px;
  color: rgb(0, 0, 0);
  font-family: Arial, sans-serif;
  font-size: 14px;
  font-weight: normal;
  overflow: hidden;
  padding: 5px 5px;
  word-break: normal;
  text-align: center;
}
.tg .tg-merge {
  background-color: #368de0;
  color: #ffffff;
  font-weight: bold;
  text-align: center;
  vertical-align: middle;
}
.tg .tg-field {
  background-color: #ffffff;
  font-weight: bold;
  text-align: center;
  vertical-align: middle;
}
.tg .tg-header {
  background-color: #475786;
  font-weight: bold;
  color: #ffffff;
  text-align: center;
  vertical-align: middle;
}
.tg .tg-footer {
  background-color: #efefef;
  text-align: center;
  vertical-align: middle;
}
</style>  