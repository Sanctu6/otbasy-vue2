<template>
  <v-container style="max-width: 100%">
    <v-row>
      <v-col cols="4">
        <v-select
          v-model="selectedProgram"
          :items="programs"
          label="Программа:"
          item-text="name"
          item-value="id"
        ></v-select></v-col
      ><v-col cols="4">
        <v-text-field
          class="inputSumm"
          v-model="summ"
          label="Сумма займа:"
          type="number"
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
          <th class="tg-header">Вид заема</th>
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
            {{ new Intl.NumberFormat().format(loan.contractSum) }} т
          </th>
        </tr>
        <tr>
          <td class="tg-field">Сумма заема</td>
          <td class="tg">{{ new Intl.NumberFormat().format(summ) }} т</td>
          <td class="tg">{{ new Intl.NumberFormat().format(summ) }} т</td>
          <td class="tg">{{ new Intl.NumberFormat().format(summ) }} т</td>
          <td class="tg">{{ new Intl.NumberFormat().format(summ) }} т</td>
          <td class="tg">{{ new Intl.NumberFormat().format(summ) }} т</td>
        </tr>
        <tr>
          <td class="tg-field">Общий срок кредитования</td>
          <td class="tg" v-for="loan in loans" :key="loan.id">
            {{ loan.fullPeriod }}
          </td>
        </tr>
        <tr>
          <td class="tg-field">Ежемесячный платеж не более</td>
          <td class="tg" v-for="loan in loans" :key="loan.id">
            {{ monthlyPay * loan.monthlyPayNoOver }}
          </td>
        </tr>
        <tr>
          <td class="tg-field">Переплата</td>
          <td class="tg" v-for="loan in loans" :key="loan.id">
            {{ summ * loan.overPay }}
          </td>
        </tr>
        <tr>
          <td class="tg-merge" colspan="6">Начальные параметры</td>
        </tr>
        <tr>
          <td class="tg-field">ЧСД| ОД</td>
          <td class="tg-field" v-for="loan in loans" :key="loan.id">
            {{ loan.chsdOd }}
          </td>
        </tr>
        <tr>
          <td class="tg-field">Срок без перехода на Жилзайм</td>
          <td class="tg" v-for="loan in loans" :key="loan.id">
            {{ loan.strokBez }}
          </td>
        </tr>
        <tr>
          <td class="tg-field">Ежемесячный платеж</td>
          <td class="tg-field" v-for="loan in loans" :key="loan.id">
            {{ monthlyPay * loan.monthlyPayNoOver }}
          </td>
        </tr>
        <tr>
          <td class="tg-field">Переход на Жилзайм (мин. ОП)</td>
          <td class="tg-field" v-for="loan in loans" :key="loan.id">
            {{ loan.perehod }}
          </td>
        </tr>
        <tr>
          <td class="tg-field">Ставка вознаграждения</td>
          <td class="tg-field">11.50%</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-field">Метод погашения</td>
          <td class="tg">Погашение % без ОД</td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
          <td class="tg"></td>
        </tr>
        <tr>
          <td class="tg-merge" colspan="6">Жилищный заем</td>
        </tr>
        <tr>
          <td class="tg-field">Срок жилищного заема</td>
          <td class="tg-field" v-for="loan in loans" :key="loan.id">
          {{ loan.strokZaema }} мес.</td>
        </tr>
        <tr>
          <td class="tg-field">Ежемесячный платеж</td>
          <td class="tg" v-for="loan in loans" :key="loan.id">
          {{ new Intl.NumberFormat().format(monthlyPay) }} т</td>
        </tr>
        <tr>
          <td class="tg-field">Ставка вознаграждения</td>
          <td class="tg" v-for="loan in loans" :key="loan.id">
          {{ loan.stavka }}.00%</td>
        </tr>
        <tr>
          <td class="tg-field">Метод погашения</td>
          <td class="tg-field" style="color:green">Аннуетет</td>
          <td class="tg-field" style="color:green">Аннуетет</td>
          <td class="tg-field" style="color:green">Аннуетет</td>
          <td class="tg-field" style="color:green">Аннуетет</td>
          <td class="tg-field" style="color:green">Аннуетет</td>
        </tr>
        <tr>
          <td class="tg-merge" colspan="6">Дополнительно</td>
        </tr>
        <tr>
          <td class="tg-field">Необходимо доложить</td>
          <td class="tg">0.00 т</td>
          <td class="tg">0.00 т</td>
          <td class="tg">0.00 т</td>
          <td class="tg">0.00 т</td>
          <td class="tg">0.00 т</td>
        </tr>
        <tr>
          <td class="tg-field">
            Ориентировочные накопления в период обеспечения вкладом
          </td>
          <td class="tg" v-for="loan in loans" :key="loan.id">
          {{ summ*loan.orient }} т</td>
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
      loans: [
        {
          id: 1,
          name: 'Пром. жилищный заем "Жеціл"',
          contractSum: 20500000,
          fullPeriod: "6 лет 6 мес.",
          monthlyPayNoOver: 1.1,
          overPay: 0.1,
          chsdOd: "251 791.67 т |39/80",
          strokBez: "108 мес.",
          perehod: "19 мес. (16 ОП)",
          strokZaema: 59,
          stavka: 5,
          orient: 0.15,
        },
        {
          id: 2,
          name: 'Пром. жилищный заем "Жеціл-2"',
          contractSum: 20500000,
          fullPeriod: "6 лет 6 мес.",
          monthlyPayNoOver: 1.1,
          overPay: 0.2,
          chsdOd: "251 791.67 т |39/80",
          strokBez: "108 мес.",
          perehod: "19 мес. (16 ОП)",
          strokZaema: 59,
          stavka: 5,
          orient: 0.15,
        },
        {
          id: 3,
          name: "Промежуточный жилищный заем",
          contractSum: 20500000,
          fullPeriod: "6 лет 6 мес.",
          monthlyPayNoOver: 1.1,
          overPay: 0.2,
          chsdOd: "251 791.67 т |39/80",
          strokBez: "108 мес.",
          perehod: "19 мес. (16 ОП)",
          strokZaema: 59,
          stavka: 5,
          orient: 0.15,
        },
        {
          id: 4,
          name: "Предварительный жилищный заем",
          contractSum: 0,
          fullPeriod: "6 лет 6 мес.",
          monthlyPayNoOver: 1.1,
          overPay: 0.2,
          chsdOd: "251 791.67 т |39/80",
          strokBez: "108 мес.",
          perehod: "19 мес. (16 ОП)",
          strokZaema: 59,
          stavka: 5,
          orient: 0.15,
        },
        {
          id: 5,
          name: "Жилищный заем",
          contractSum: 20500000,
          fullPeriod: "6 лет 6 мес.",
          monthlyPayNoOver: 1.1,
          overPay: 0.2,
          chsdOd: "251 791.67 т |39/80",
          strokBez: "108 мес.",
          perehod: "19 мес. (16 ОП)",
          strokZaema: 59,
          stavka: 5,
          orient: 0.15,
        },
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
  font-family: Arial, sans-serif;
  font-size: 11px;
  text-align: center;
  padding: 5px 5px;
  vertical-align: middle;
}
.tg td {
  background-color: #ffffff;
  border-color: #9abad9;
  border-style: solid;
  border-width: 1px;
  color: #444;
  overflow: hidden;
  word-break: normal;
}
.tg th {
  background-color: #ffffff;
  border-color: #9abad9;
  border-style: solid;
  border-width: 1px;
  color: rgb(0, 0, 0);
  font-weight: normal;
  overflow: hidden;
  padding: 5px 5px;
}
.tg .tg-merge {
  text-transform: uppercase;
  letter-spacing: 0.2rem;
  background-color: #368de0;
  color: #ffffff;
  font-weight: bold;
}
.tg .tg-field {
  background-color: #ffffff;
  font-weight: bold;
}
.tg .tg-header {
  background-color: #475786;
  font-weight: bold;
  color: #ffffff;
}
.tg .tg-footer {
  background-color: #efefef;
}
</style>  