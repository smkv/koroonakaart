<template>
  <b-container id="statsbar-container" class="mb-5" fluid>
    <b-row>
      <b-col class="statsbar-item" md>
        <div class="statsbar-heading">
          <h5>{{ $t("confirmedCases") }}</h5>
        </div>
        <h1>{{confirmedCasesNumber}}</h1>
        <h5 :class="rawConfirmedChanged > 0 ? 'positive' : 'negative'">( {{confirmedChanged}} )</h5>
      </b-col>

      <b-col class="statsbar-item" md>
        <div class="statsbar-heading">
          <h5>{{ $t("activeCases") }}</h5>
        </div>
        <h1>{{activeCasesNumber}}</h1>
        <h5 :class="rawActiveChanged > 0 ? 'positive' : 'negative'">( {{activeChanged}} )</h5>
      </b-col>

      <b-col class="statsbar-item" md>
        <div class="statsbar-heading">
          <h5>{{ $t("testsAdministered") }}</h5>
        </div>
        <h1>{{testsAdministeredNumber}}</h1>
        <h5
          :class="rawTestsChanged === 0 ? 'neutral' : rawTestsChanged > 0 ? 'negative' : 'positive'"
        >( {{testsChanged}} )</h5>
      </b-col>


</b-row>
<br>
<b-row>
<b-col class="statsbar-item" md>
  <div class="statsbar-heading">
    <h5>{{ $t("hospitalised") }}</h5>
  </div>
  <h1>{{hospitalisedNumber}}</h1>
  <h5
    :class="rawHospitalisedChanged === 0 ? 'neutral' : rawHospitalisedChanged > 0 ? 'positive' : 'negative'"
  >( {{hospitalisedChanged}} )</h5>
</b-col>

<b-col class="statsbar-item" md>
  <div class="statsbar-heading">
    <h5>{{ $t("recovered") }}</h5>
  </div>
  <h1>{{recoveredNumber}}</h1>
  <h5
    :class="rawRecoveredChanged === 0 ? 'neutral' : rawRecoveredChanged > 0 ? 'negative' : 'positive'"
  >( {{recoveredChanged}} )</h5>
</b-col>

      <b-col class="statsbar-item" md>
        <div class="statsbar-heading">
          <h5>{{ $t("deceased") }}</h5>
        </div>
        <h1>{{deceasedNumber}}</h1>
        <h5
          :class="rawDeceasedChanged === 0 ? 'neutral' : rawDeceasedChanged > 0 ? 'positive' : 'negative'"
        >( {{deceasedChanged}} )</h5>
      </b-col>




    </b-row>
  </b-container>
</template>

<script>
import data from "../data.json";
import { positiveSign } from "../utilities/helper";
export default {
  name: "Statsbar",

  data() {
    return {
      confirmedCasesNumber: data.confirmedCasesNumber,
      activeCasesNumber: data.activeCasesNumber,
      activeChanged: positiveSign(data.activeChanged),
      rawActiveChanged: data.dataCumulativeCasesChart.active[
        data.dataCumulativeCasesChart.active.length - 1
      ]  -
      data.dataCumulativeCasesChart.active[
        data.dataCumulativeCasesChart.active.length - 2
      ],
      hospitalisedNumber: data.hospitalisedNumber,
      deceasedNumber: data.deceasedNumber,
      recoveredNumber: data.recoveredNumber,
      testsAdministeredNumber: data.testsAdministeredNumber,
      rawHospitalisedChanged: data.hospitalChanged,
      rawRecoveredChanged: data.recoveredChanged,
      rawDeceasedChanged: data.deceasedChanged,
      rawConfirmedChanged:
        data.dataNewCasesPerDayChart.confirmedCases[
          data.dataNewCasesPerDayChart.confirmedCases.length - 1
        ],
      rawTestsChanged:
        data.dataCumulativeTestsChart.testsAdminstered[
          data.dataCumulativeTestsChart.testsAdminstered.length - 1
        ] -
        data.dataCumulativeTestsChart.testsAdminstered[
          data.dataCumulativeTestsChart.testsAdminstered.length - 2
        ],
      hospitalisedChanged: positiveSign(data.hospitalChanged),
      recoveredChanged: positiveSign(data.recoveredChanged),
      deceasedChanged: positiveSign(data.deceasedChanged),
      confirmedChanged: positiveSign(
        data.dataNewCasesPerDayChart.confirmedCases[
          data.dataNewCasesPerDayChart.confirmedCases.length - 1
        ]
      ),
      testsChanged: positiveSign(
        data.dataCumulativeTestsChart.testsAdminstered[
          data.dataCumulativeTestsChart.testsAdminstered.length - 1
        ] -
          data.dataCumulativeTestsChart.testsAdminstered[
            data.dataCumulativeTestsChart.testsAdminstered.length - 2
          ]
      )
    };
  }
};
</script>

<style lang="scss" scoped>
#statsbar-container {
  @media only screen and (max-width: 766px) {
    margin-bottom: 0;
  }
}

.statsbar-heading {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 4em;
  margin-bottom: -0.5em;
}

.positive {
  color: red;
}

.negative {
  color: green;
}

.neutral {
  color: rgb(97, 97, 97);
}

.statsbar-item {
  //  height: 7em;

  @media only screen and (max-width: 766px) {
    margin-bottom: 1em;
  }
}
</style>
