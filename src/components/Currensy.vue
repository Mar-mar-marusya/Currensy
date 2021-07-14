<template>
  <el-row :gutter="20" justify="space-around" >
    <el-col :span="4" style="margin-left: 20px"
      ><div class="grid-content bg-purple">
        <el-select
          no-data-text="Нет данных"
          v-model="selectedCurrency"
          placeholder="Выберите валюту"
          clearable
          @change="selectCurrency($event)"
        >
          <el-option
            v-for="item in aCurrensies"
            :key="item.ID"
            :label="item.CharCode"
            :value="item.CharCode"
          >
            <span style="float: left; margin-right: 20px; width: 50px">{{
              item.CharCode
            }}</span>
            <span style="float: left; margin-right: 20px">{{ item.Name }}</span>
            <span style="float: right; color: #8492a6; font-size: 13px">{{
              item.Value
            }}</span>
          </el-option>
        </el-select>
      </div></el-col
    >
    <el-col :span="4">
      <div class="grid-content bg-purple">
        <el-input
          v-model="currensyData.value"
          placeholder="Введите сумму в рублях"
        ></el-input></div
    ></el-col>
    <el-col :span="5">
      <div class="grid-content bg-purple align-center spaceBottom">
          <a class="align-center">Коэффициент {{ currensyData.currensy.Value }}</a>
      </div>
    </el-col>
    <el-col :span="5">
      <div class="grid-content bg-purple align-center spaceBottom">
        Номинал {{ currensyData.currensy.Nominal }}
      </div>
    </el-col>
    <el-col :span="5">
      <div class="grid-content bg-purple align-center spaceBottom">
        {{ calculatedValue }}
      </div></el-col
    >
  </el-row>
</template>

<script>
export default {
  beforeMount() {
    this.getCurrencies();
  },
  name: "Currensy",
  props: {},
  data: function () {
    return {
      currensyData: {
        currensy: {
          CharCode: "",
          ID: "",
          Name: "",
          Nominal: "",
          NumCode: "",
          Previous: "",
          Value: "",
        },
        value: "",
      },
      aCurrensies: [
        {
          CharCode: "",
          ID: "",
          Name: "",
          Nominal: "",
          NumCode: "",
          Previous: "",
          Value: "",
        },
      ],
      selectedCurrency: "",
    };
  },
  methods: {
    getCurrencies: async function () {
      const response = await fetch(
          "https://www.cbr-xml-daily.ru/daily_json.js"
        ),
        jsonResponse = await response.json(),
        result = await jsonResponse;

      this.aCurrensies = [];
      for (const key in result.Valute) {
        this.aCurrensies.push(result.Valute[key]);
      }
      console.log(`получился массив: ${JSON.stringify(this.aCurrensies)}`);
    },
    selectCurrency(event) {
      console.log(event);
      let oSelectedCurrency = this.aCurrensies.find(
        (el) => el.CharCode === event
      );
      this.currensyData.currensy = oSelectedCurrency;
    },
  },
  computed: {
    // геттер вычисляемого значения
    calculatedValue: function () {
      // `this` указывает на экземпляр vm
      return this.currensyData.value
        ? `Сумма в выбранной валюте ${(
            (this.currensyData.value * this.currensyData.currensy.Nominal) /
            this.currensyData.currensy.Value
          ).toFixed(2)}`
        : "Не введена сумма в рублях";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.el-row {
  margin-bottom: 20px;
}
.el-col {
  border-radius: 4px;
}
.bg-purple-dark {
  background: #99a9bf;
}
.bg-purple {
  background: #d3dce6;
}
.bg-purple-light {
  background: #e5e9f2;
}
.grid-content {
  border-radius: 4px;
  min-height: 16px;
}
.row-bg {
  padding: 10px 0;
  background-color: #f9fafc;
}
.align-center {
  padding: 10px;
}
.spaceBottom {
  margin-bottom: 20px;
}
</style>
