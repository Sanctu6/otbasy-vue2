<template>
  <v-container>
    <v-label>Выбирете займ</v-label>
    <v-container>
      <v-row>
        <v-col cols="4">
          <v-select v-model="selectedProgram" :items="programs" label="Программа:" item-text="name" item-value="id"
            dense></v-select></v-col><v-col cols="4">
          <v-text-field v-model="summ" label="Сумма займа:" type="number" dense></v-text-field></v-col><v-col cols="4">
          <v-label>Ежемес. платеж:</v-label>
          <v-slider v-model="monthlyPay" track-color="grey" color="green" always-dirty min="10000" :max="summ"
            step="10000" dense>
            <template v-slot:prepend>
              <v-icon @click="decrement"> mdi-minus </v-icon>
            </template>

            <template v-slot:append>
              <v-icon @click="increment"> mdi-plus </v-icon>
            </template>
          </v-slider>
        </v-col>
      </v-row></v-container>
    <table class="tg">
      <thead>
        <tr>
          <th class="tg-baqh">Вид займа</th>
          <th class="tg-baqh" v-for="loan in loans" :key="loan.id">
            {{ loan.name }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td class="tg-baqh" colspan="6">Общие сведения</td>
        </tr>
        <tr>
          <td class="tg-baqh">Договорная сумма</td>
          <th class="tg-baqh" v-for="loan in loans" :key="loan.id">
            {{ loan.contractSum }}
          </th>
        </tr>
        <tr>
          <td class="tg-baqh">сумма</td>
          <td class="tg-baqh">{{ summ }}</td>
          <td class="tg-baqh">{{ summ }}</td>
          <td class="tg-baqh">{{ summ }}</td>
          <td class="tg-baqh">{{ summ }}</td>
          <td class="tg-baqh">{{ summ }}</td>
        </tr>
        <tr>
          <td class="tg-baqh">общий</td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
        </tr>
        <tr>
          <td class="tg-baqh">Ежемеся</td>
          <td class="tg-baqh">{{ monthlyPay }}</td>
          <td class="tg-baqh">{{ monthlyPay }}</td>
          <td class="tg-baqh">{{ monthlyPay }}</td>
          <td class="tg-baqh">{{ monthlyPay }}</td>
          <td class="tg-baqh">{{ monthlyPay }}</td>
        </tr>
        <tr>
          <td class="tg-baqh">переплата</td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
        </tr>
        <tr>
          <td class="tg-baqh" colspan="6">Начальные</td>
        </tr>
        <tr>
          <td class="tg-baqh">ЧСД</td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
        </tr>
        <tr>
          <td class="tg-baqh">Срок без</td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
        </tr>
        <tr>
          <td class="tg-baqh">Ежемеся</td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
        </tr>
        <tr>
          <td class="tg-baqh">Переход</td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
        </tr>
        <tr>
          <td class="tg-baqh">Ставка</td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
        </tr>
        <tr>
          <td class="tg-baqh">Метод</td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
        </tr>
        <tr>
          <td class="tg-baqh" colspan="6">Жилищный</td>
        </tr>
        <tr>
          <td class="tg-baqh">Срок жилищ</td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
        </tr>
        <tr>
          <td class="tg-baqh">Ежемесячный</td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
        </tr>
        <tr>
          <td class="tg-baqh">Ставка</td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
        </tr>
        <tr>
          <td class="tg-baqh">Метод</td>
          <td class="tg-baqh">Аннуетет</td>
          <td class="tg-baqh">Аннуетет</td>
          <td class="tg-baqh">Аннуетет</td>
          <td class="tg-baqh">Аннуетет</td>
          <td class="tg-baqh">Аннуетет</td>
        </tr>
        <tr>
          <td class="tg-baqh" colspan="6">Дополнительно</td>
        </tr>
        <tr>
          <td class="tg-baqh">Необходимо</td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
        </tr>
        <tr>
          <td class="tg-baqh">Ориентировочные</td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
          <td class="tg-baqh"></td>
        </tr>
        <tr>
          <td class="tg-baqh"></td>
          <td class="tg-baqh">
            <v-btn color="primary"><v-icon left>mdi-check-circle-outline</v-icon> Выбрать</v-btn>
          </td>
          <td class="tg-baqh">
            <v-btn color="primary"><v-icon left>mdi-check-circle-outline</v-icon> Выбрать</v-btn>
          </td>
          <td class="tg-baqh">
            <v-btn color="primary"><v-icon left>mdi-check-circle-outline</v-icon> Выбрать</v-btn>
          </td>
          <td class="tg-baqh">
            <v-btn color="orange" disabled><v-icon left dark>mdi-close-circle-outline</v-icon> Не
              доступен</v-btn>
          </td>
          <td class="tg-baqh">
            <v-btn color="orange" disabled><v-icon left dark>mdi-close-circle-outline</v-icon> Не
              доступен</v-btn>
          </td>
        </tr>
      </tbody>
    </table>
  </v-container>
</template>
<script>
export default {
  name: "TransposeTable",
  created() {
    console.log("Starting connection to WebSocket Server");
    this.connection = new WebSocket("ws://localhost:8081");

    //THAT WORKS
    this.result = "Result of command";

    this.connection.onmessage = (event) => {
      console.log(event);
    };
    this.connection.onopen = function (event) {
      console.log(event);
      console.log("Successfully connected to the echo websocket server...");
    };
  },
  data() {
    return {
      connection: null,
      summ: 20500000,
      monthlyPay: 500000,
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
  },
};
</script>
<style scoped>
.tg {
  border-collapse: collapse;
  border-spacing: 0;
}

.tg td {
  border-color: rgb(0, 0, 0);
  border-style: solid;
  border-width: 1px;
  font-family: Arial, sans-serif;
  font-size: 14px;
  overflow: hidden;
  padding: 5px 5px;
  word-break: normal;
}

.tg th {
  border-color: rgb(0, 0, 0);
  border-style: solid;
  border-width: 1px;
  font-family: Arial, sans-serif;
  font-size: 14px;
  font-weight: normal;
  overflow: hidden;
  padding: 5px 5px;
  word-break: normal;
}

.tg .tg-baqh {
  text-align: center;
  vertical-align: top;
}
</style>  