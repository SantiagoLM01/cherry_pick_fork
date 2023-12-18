<script setup lang="ts">
import { useBreakpoints } from "../composables/breakpoints";

const {
  phones_breakpoint,
  tablets_breakpoint,
  laptops_breakpoint,
  desktops_breakpoint,
} = useBreakpoints();

const { t } = useI18n({ useScope: "local" });

import UITableNew from "./UITableNew.vue";
const data = [
  {
    method: "Cryptocurrency",
    availability: "Global",
    "minimum-withdrawal": "$50",
    active: true,
    currencies: "USDT (ERC20 & TRC20)",
    "maximum-withdrawal": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
  },
  {
    method: "Bank Wire",
    availability: "Global, except China Mainland",
    "minimum-withdrawal": "$50",
    active: false,
    currencies: "USDT (ERC20 & TRC20)",
    "maximum-withdrawal": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
  },
  {
    method: "China Union Pay",
    availability: "China Mainland",
    "minimum-withdrawal": "$50",
    active: false,
    currencies: "USDT (ERC20 & TRC20)",
    "maximum-withdrawal": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
  },
  {
    method: "Credit Card",
    availability: "Global",
    "minimum-withdrawal": "$50",
    active: false,
    currencies: "USDT (ERC20 & TRC20)",
    "maximum-withdrawal": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
  },
  {
    method: "Dragonpay",
    availability: "Philippines",
    "minimum-withdrawal": "$50",
    active: false,
    currencies: "USDT (ERC20 & TRC20)",
    "maximum-withdrawal": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
  },
  {
    method: "FASA",
    availability: "Indonesia",
    "minimum-withdrawal": "$50",
    active: false,
    currencies: "USDT (ERC20 & TRC20)",
    "maximum-withdrawal": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
  },
  {
    method: "Neteller",
    availability: "Global, except Europe",
    "minimum-withdrawal": "$50",
    active: false,
    currencies: "USDT (ERC20 & TRC20)",
    "maximum-withdrawal": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
  },
  {
    method: "Paytrust",
    availability: "Indonesia, Malaysia, Vietnam",
    "minimum-withdrawal": "$50",
    active: false,
    currencies: "USDT (ERC20 & TRC20)",
    "maximum-withdrawal": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
  },
  {
    method: "Perfect Money",
    availability: "Global",
    "minimum-withdrawal": "$50",
    active: false,
    currencies: "USDT (ERC20 & TRC20)",
    "maximum-withdrawal": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
  },
  {
    method: "Skrill",
    availability: "Global, except Europe",
    "minimum-withdrawal": "$50",
    active: false,
    currencies: "USDT (ERC20 & TRC20)",
    "maximum-withdrawal": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
  },
  {
    method: "SticPay",
    availability: "Global",
    "minimum-withdrawal": "$50",
    active: false,
    currencies: "USDT (ERC20 & TRC20)",
    "maximum-withdrawal": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
  },
  {
    method: "THB QR Payment",
    availability: "Thailand",
    "minimum-withdrawal": "$50",
    active: false,
    currencies: "USDT (ERC20 & TRC20)",
    "maximum-withdrawal": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
  },
];
</script>

<template>
  <!--TITLE SEC-->
  <div>
    <GridContainer>
      <div
        class="col-span-12 col-start-1 col-end-13 tablets:col-span-10 tablets:col-start-2 tablets:col-end-12 laptops:col-span-8 laptops:col-start-3 laptops:col-end-11"
      >
        <div class="text-center flex justify-center">
          <UIHeading heading_size="m" class="">
            <slot name="title-sec"></slot>
          </UIHeading>
        </div>

        <div
          class="text-center mt-spacing-100 tablets:mt-spacing-125 laptops:mt-spacing-100"
        >
          <span
            class="font-secondary text-[1.125rem] font-fx-bold leading-[1.22] tracking-[0.32px] text-center"
          >
            <slot name="content-sec"
              >Focus on mastering the markets, and we’ll take care of the rest.
              Invest without worrying about commissions on your deposit. Enjoy a
              commission free trading experience.</slot
            >
          </span>
        </div>
      </div>
      <div class="col-span-12 col-start-1 col-end-13">
        <UITableNew
          :row="8"
          :isPaginated="true"
          :data="data"
          v-slot="slotProps"
          :oddColorChange="true"
          :hover="true"
          activePropertyName="active"
          translationPath="sections.withdrawals.instance-1.table1"

        >
          <Column
            field="method"
            :header="t('sections.deposits.instance-1.table1.method')"
            :value="slotProps"
          ></Column>
          <Column
            field="availability"
            :header="t('sections.deposits.instance-1.table1.availability')"
            :value="slotProps"
          ></Column>
          <Column
            field="currencies"
            :header="t('sections.deposits.instance-1.table1.currencies')"
            :value="slotProps"
          ></Column>
          <Column
            field="minimum-withdrawal"
            :header="t('sections.deposits.instance-1.table1.minimum-deposit')"
            :value="slotProps"
          ></Column>
          <Column
            field="maximum-withdrawal"
            :header="t('sections.deposits.instance-1.table1.maximum-deposit')"
            :value="slotProps"
          ></Column>
          <Column
            field="processing-time"
            :header="t('sections.deposits.instance-1.table1.processing-time')"
            :value="slotProps"
          ></Column>
          <Column
            field="fees"
            :header="t('sections.deposits.instance-1.table1.fees')"
            :value="slotProps"
          ></Column>
        </UITableNew>
      </div>
    </GridContainer>
  </div>
</template>
