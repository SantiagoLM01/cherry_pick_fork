<script setup lang="ts">
import { useBreakpoints } from "../composables/breakpoints";
import UITableNew from "./UITableNew.vue";

const { t, locale } = useI18n({ useScope: 'local' })


const {
  phones_breakpoint,
  tablets_breakpoint,
  laptops_breakpoint,
  desktops_breakpoint,
} = useBreakpoints();

const data = [
  {
    method: "Cryptocurrency",
    availability: "Global",
    currencies: "USDT (ERC20 & TRC20)",
    "minimum-deposit": "$50",
    "maximum-deposit": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
    active: true,
  },
  {
    method: "Bank Wire",
    availability: "Global, except China Mainland",
    currencies: "USDT (ERC20 & TRC20)",
    "minimum-deposit": "$50",
    "maximum-deposit": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
    active: false,
  },
  {
    method: "China Union Pay",
    availability: "China Mainland",
    currencies: "USDT (ERC20 & TRC20)",
    "minimum-deposit": "$50",
    "maximum-deposit": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
    active: false,
  },
  {
    method: "Credit Card",
    availability: "Global",
    currencies: "USDT (ERC20 & TRC20)",
    "minimum-deposit": "$50",
    "maximum-deposit": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
    active: false,
  },
  {
    method: "Dragonpay",
    availability: "Philippines",
    currencies: "USDT (ERC20 & TRC20)",
    "minimum-deposit": "$50",
    "maximum-deposit": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
    active: false,
  },
  {
    method: "FASA",
    availability: "Indonesia",
    currencies: "USDT (ERC20 & TRC20)",
    "minimum-deposit": "$50",
    "maximum-deposit": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
    active: false,
  },
  {
    method: "Neteller",
    availability: "Global, except Europe",
    currencies: "USDT (ERC20 & TRC20)",
    "minimum-deposit": "$50",
    "maximum-deposit": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
    active: false,
  },
  {
    method: "Paytrust",
    availability: "Indonesia, Malaysia, Vietnam",
    currencies: "USDT (ERC20 & TRC20)",
    "minimum-deposit": "$50",
    "maximum-deposit": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
    active: false,
  },
  {
    method: "Perfect Money",
    availability: "Global",
    currencies: "USDT (ERC20 & TRC20)",
    "minimum-deposit": "$50",
    "maximum-deposit": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
    active: false,
  },
  {
    method: "Skrill",
    availability: "Global, except Europe",
    currencies: "USDT (ERC20 & TRC20)",
    "minimum-deposit": "$50",
    "maximum-deposit": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
    active: false,
  },
  {
    method: "STICPAY",
    availability: "Global",
    currencies: "USDT (ERC20 & TRC20)",
    "minimum-deposit": "$50",
    "maximum-deposit": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
    active: false,
  },
  {
    method: "THB QR Payment",
    availability: "Thailand",
    currencies: "USDT (ERC20 & TRC20)",
    "minimum-deposit": "$50",
    "maximum-deposit": "$50,000",
    "processing-time": "Within 24 hours",
    fees: "$0",
    active: false,
  },
];
</script>

<template>
  <!--TITLE SEC-->
  <div>
    <GridContainer>
      <div
        class="col-span-12 col-start-1 col-end-13 tablets:col-span-10 tablets:col-start-2 tablets:col-end-12 laptops:col-span-8 laptops:col-start-3 laptops:col-end-"
      >
        <div class="text-center flex justify-center">
          <UIHeading heading_size="m">
            <slot name="title-sec"></slot>
          </UIHeading>
        </div>
        <div
          class="text-center mt-spacing-100 tablets:mt-spacing-125 laptops:mt-spacing-100"
        >
          <span
            class="font-secondary text-[1.125rem] font-fx-bold leading-[1.22] tracking-[0.32px]"
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
          translationPath="sections.deposits.instance-1.table1"

        >
          <Column field="method" :header="t('sections.deposits.instance-1.table1.method')" :value="slotProps"></Column>
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
            field="minimum-deposit"
            :header="t('sections.deposits.instance-1.table1.minimum-deposit')"
            :value="slotProps"
          ></Column>
          <Column
            field="maximum-deposit"
            :header="t('sections.deposits.instance-1.table1.maximum-deposit')"
            :value="slotProps"
          ></Column>
          <Column
            field="processing-time"
            :header="t('sections.deposits.instance-1.table1.processing-time')"
            :value="slotProps"
          ></Column>
          <Column field="fees" :header="t('sections.deposits.instance-1.table1.fees')" :value="slotProps"></Column>
        </UITableNew>
      </div>
    </GridContainer>
  </div>
</template>
