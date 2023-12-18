<script setup lang="ts">

const { t, locale } = useI18n({ useScope: "local" });

useSeoMeta({
  title: t("titles.withdrawals-and-deposits"),
});
</script>

<template>
  <!--HEADER 3-->
  <SectionHeader-3 class="bg-[url(/img/header/header-3/instance-1-bg.png)] bg-cover">
    <template #main-title-sec><span class="bg-gradient-to-r from-[#8640FF] to-[#4DACFE] inline-block text-transparent bg-clip-text">{{ t("sections.header-3.instance-1.main-title") }}</span></template>
    <template #sub-title-sec>{{ t("sections.header-3.instance-1.sub-title") }}</template>
    <template #content-sec><span class="text-[#687684]">{{ t("sections.header-3.instance-1.content") }}</span></template>
  </SectionHeader-3>
  <!--HEADER 3-->


  <div class="bg-[url(/img/deposits/deposits-1/instance-1-bg.png)]  bg-cover bg-no-repeat pt-12 laptops:py-16">
    <!--DEP ADN WITHDR-->
    <SectionDeposits>
      <template #title-sec>{{ t("sections.deposits.instance-1.main-title") }}</template>
      <template #content-sec><span class="text-[#687684]">{{ t("sections.deposits.instance-1.content") }}</span></template>
    </SectionDeposits>
  </div>
  
  <div class="bg-[url(/img/withdrawals/withdrawals-1/instance-1-bg.png)]  bg-cover bg-no-repeat pt-12 laptops:py-16">
    <SectionWithdrawals>
      <template #title-sec>{{ t("sections.withdrawals.instance-1.main-title") }}</template>
      <template #content-sec><span class="text-[#687684]">{{ t("sections.withdrawals.instance-1.content") }}</span></template>
    </SectionWithdrawals>
  </div>

  
  <!--DEP ADN WITHDR-->


  <!--ACADEMY 1-->
  <!--<SectionAcademy1>
    <template #top-title><span class="text-[#3430f5]">{{ t("section-academy-1-toptitle") }}</span></template>
    <template #main-title>{{ t("section-academy-1-maintitle") }}</template>
  </SectionAcademy1>-->
  <!--ACADEMY 1-->
  <!--SectionAcademy-2-new-1-->
  <div class="bg-[url(/img/academy/academy-2-new/instance-1-bg.png)] bg-cover bg-no-repeat pt-10">
    <SectionAcademy-2-new-1>
    <template #top-title><span class="text-[#416dff]">{{ t("sections.academy-2-new.instance-1.top-title") }}</span></template>
    <template #main-title>{{ t("sections.academy-2-new.instance-1.main-title") }}</template>
    <template #card1>{{ t("sections.academy-2-new.instance-1.card1-title") }}</template>
    <template #card2>{{ t("sections.academy-2-new.instance-1.card2-title") }}</template>
    <template #card3>{{ t("sections.academy-2-new.instance-1.card3-title") }}</template>
    <template #card1-content>{{ t("sections.academy-2-new.instance-1.card1-content") }}</template>
    <template #card2-content>{{ t("sections.academy-2-new.instance-1.card2-content") }}</template>
    <template #card3-content>{{ t("sections.academy-2-new.instance-1.card3-content") }}</template>
  </SectionAcademy-2-new-1>
  </div>


  <div class="bg-[url(/img/faq/faq-1/instance-1-bg.png)] bg-cover bg-no-repeat">
    <SectionFAQ1 >
      <template #top-title-sec><span class="text-[#416dff]">{{ t("sections.FAQ-1.instance-1.top-title") }}</span></template>
      <template #main-title-sec>{{ t("sections.FAQ-1.instance-1.main-title") }}</template>
      <template #main-content-sec></template>
      <template #button-texts>{{ t("sections.FAQ-1.instance-1.button-text") }}</template>
      <template #dis-1-main-content>{{ t("sections.FAQ-1.instance-1.Q1") }}</template>
      <template #dis-1-drop-content>{{ t("sections.FAQ-1.instance-1.AQ1") }}</template>
      <template #dis-2-main-content>{{ t("sections.FAQ-1.instance-1.Q2") }}</template>
      <template #dis-2-drop-content>{{ t("sections.FAQ-1.instance-1.AQ2") }}</template>
      <template #dis-3-main-content>{{ t("sections.FAQ-1.instance-1.Q3") }}</template>
      <template #dis-3-drop-content>{{ t("sections.FAQ-1.instance-1.AQ3") }}</template>
      <template #dis-4-main-content>{{ t("sections.FAQ-1.instance-1.Q4") }}</template>
      <template #dis-4-drop-content>{{ t("sections.FAQ-1.instance-1.AQ4") }}</template>
    </SectionFAQ1>
    <!--FAQ-->
  </div>
  
</template>

