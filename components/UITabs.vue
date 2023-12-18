<script setup lang="ts">
import { Menu, MenuButton, MenuItems, MenuItem } from "@headlessui/vue";

const props = defineProps({
  tabs: {
    type: Array<Object>,
    required: false,
    default: [],
  },
  selectedTab: {
    type: String,
    required: false,
    default: "",
  },
  translationPath: {
    type: String,
    required: true,
  },
});

const { t } = useI18n({ useScope: "local" });

const emit = defineEmits(["changeTab"]);

const changeTab = (e) => {
  currentTab.value = e;

  emit("changeTab", e);
};

const currentTab = ref(props.selectedTab);
</script>

<template>
  <div v-if="tabs.length > 0" class="flex gap-spacing-225 justify-start">
    <div
      class="hidden tablets:block"
      v-for="(item, index) in tabs"
      :key="index"
    >
      <p
        @click="changeTab(item.name)"
        class="text-[#687684] cursor-pointer hover:text-fxblue hover:bg-[#eaeafe] px-spacing-100 rounded-xl font-bold"
        :class="item.name === currentTab ? 'text-fxblue bg-[#eaeafe] ' : null"
      >
        {{ t(`${translationPath}.${item.name.toLowerCase()}`) }}
      </p>
    </div>
    <div class="tablets:hidden w-full flex justify-center">
      <Menu
        as="div"
        class="relative inline-block text-left z-[2]"
        v-slot="{ open }"
      >
        <div>
          <MenuButton
            class="flex justify-between items-center p-spacing-150 border w-[184px] h-[48px] rounded-full"
          >
            <p class="text-[16px]">
              {{ t(`${translationPath}.${currentTab.toLowerCase()}`) }}
            </p>
            <SVGComponent
              :svgURL="'/img/misc/bigDropdownArrow.svg'"
              width="16"
              heigth="8"
              :isStroke="true"
              :class="
                open
                  ? 'rotate-180 ease-in-out duration-600 transform transition'
                  : 'rotate-0 ease-in-out duration-600 transform transition'
              "
              :color="'black'"
            />
          </MenuButton>
        </div>

        <transition
          enter-active-class="transition duration-100 ease-out"
          enter-from-class="transform scale-95 opacity-0"
          enter-to-class="transform scale-100 opacity-100"
          leave-active-class="transition duration-75 ease-in"
          leave-from-class="transform scale-100 opacity-100"
          leave-to-class="transform scale-95 opacity-0"
        >
          <MenuItems
            class="z-[-1] absolute top-4 w-[184px] pb-4 origin-top-right rounded-md bg-white shadow-lg focus:outline-none"
          >
            <div class="py-5"></div>
            <MenuItem
              @click="changeTab(item.name)"
              v-slot="{ active }"
              v-for="(item, index) in tabs"
              class="text-start px-6 cursor-pointer hover:text-fxblue"
              :class="item.name === currentTab ? 'font-bold text-fxblue' : null"
            >
              <div>
                <p class="text-[14px] my-[4px]">
                  {{ t(`${translationPath}.${item.name.toLowerCase()}`) }}
                </p>
                <hr v-if="index != tabs.length - 1" />
              </div>
            </MenuItem>
          </MenuItems>
        </transition>
      </Menu>
    </div>
  </div>
</template>
