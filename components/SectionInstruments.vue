<script setup lang="ts">
import UITableNew from "./UITableNew.vue";

const data: Ref<Object> = ref(getTableData("Overview"));

const selectedTab: Ref<String> = ref("Overview");

const changeTabData = (tabName) => {
  if (!tabName) return;

  selectedTab.value = tabName;

  data.value = getTableData(tabName);
};

const { t } = useI18n({ scoped: "local" });
</script>

<template>
  <GridContainer>
    <UITabs
      class="col-span-12 col-start-1 col-end-13"
      @changeTab="changeTabData"
      :tabs="[
        { name: 'Overview' },
        { name: 'Forex' },
        { name: 'Shares' },
        { name: 'Crypto' },
        { name: 'Commodities' },
        { name: 'Indices' },
      ]"
      :selectedTab="selectedTab"
      translationPath="sections.instruments.tabs"
    />

    <div class="col-span-12 col-start-1 col-end-13">
      <UITableNew
        theadStyle="bg-[#eaeafd]"
        v-if="selectedTab === 'Overview'"
        :subTabs="data?.subTabs"
        selectedSubTab="Majors"
        :row="8"
        :isPaginated="true"
        :data="data.data"
        v-slot="slotProps"
        :oddColorChange="true"
        :hover="true"
        translationPath="sections.instruments.table1"

      >
        <Column
          field="trading-instrument"
          header="Trading Instrument"
          :value="slotProps"
        ></Column>
        <Column
          field="spread-pt"
          header="Spread PT"
          :value="slotProps"
        ></Column>
        <Column field="link" header="" :value="slotProps">
          <UIButtonWide
            :button_link="{ path: slotProps.value.link }"
            b_style="smaller_outline"
            class="border-fxblue"
          >
            <template #button_text
              ><span class="text-fxblue">{{ t(`sections.instruments.table1.trade`)}}</span></template
            >
            <template #button_icon>
              <SVGComponent
                svgURL="/img/misc/feather-arrow-right.svg"
                :heigth="'8'"
                :isStroke="true"
                :color="'#3430f5'"
              />
            </template>
          </UIButtonWide>
        </Column>
      </UITableNew>

      <UITableNew
        v-else-if="selectedTab === 'Shares'"
        :subTabs="data?.subTabs"
        :row="8"
        :isPaginated="true"
        :data="data.data"
        v-slot="slotProps"
        :oddColorChange="true"
        :hover="true"
        translationPath="sections.instruments.table3"

      >
        <Column field="symbol" header="Symbol" :value="slotProps"></Column>
        <Column field="name" header="Name" :value="slotProps"></Column>
        <Column
          field="trading-hours"
          header="Trading Hours"
          :value="slotProps"
        ></Column>
      </UITableNew>
      <UITableNew
        v-else
        :subTabs="data?.subTabs"
        :row="8"
        :isPaginated="true"
        :data="data.data"
        v-slot="slotProps"
        :oddColorChange="true"
        :hover="true"
        translationPath="sections.instruments.table2"

      >
        <Column field="symbol" header="Symbol" :value="slotProps"></Column>
        <Column field="name" header="Name" :value="slotProps"></Column>
        <Column
          field="min-spreads"
          header="Min Spreads"
          :value="slotProps"
        ></Column>
        <Column
          field="typical-spreads"
          header="Typical spreads"
          :value="slotProps"
        ></Column>
        <Column
          field="swap-short"
          header="Swap Short"
          :value="slotProps"
        ></Column>
        <Column
          field="swap-long"
          header="Swap Long"
          :value="slotProps"
        ></Column>
        <Column
          field="trading-hours"
          header="Trading Hours"
          :value="slotProps"
        ></Column>
      </UITableNew>
    </div>
  </GridContainer>
</template>
