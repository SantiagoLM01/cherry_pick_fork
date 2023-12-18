<script setup lang="ts">
import { PropType } from "nuxt/dist/app/compat/capi";
import { defineProps, onMounted, ref } from "vue";
import { useSlots } from "vue";

const { t } = useI18n({ scoped: "locals" });

const props = defineProps({
  data: {
    type: Array,
    required: true,
    default: () => [],
  },
  row: {
    type: Number,
    required: false,
  },

  oddColorChange: {
    type: Boolean,
    required: false,
  },
  isPaginated: {
    type: Boolean,
    required: false,
  },
  hover: {
    type: Boolean,
    required: false,
  },
  subTabs: {
    type: Array<Object>,
    required: false,
    default: [],
  },
  selectedSubTab: {
    type: String,
    default: "",
  },
  theadStyle: {
    type: String,
    default: "",
    required: false,
  },
  activePropertyName: {
    type: String as PropType<String>,
    default: "",
    required: false,
  },
  translationPath: {
    type: String as PropType<String>,
    required: true,
  },
});

const slots = useSlots();

const columns = ref([]);

const pagination = reactive({
  currentPage: 1,
  maxPages: 1,
});

const leftPaginationButton = ref(1);

const midPaginationButton = ref(2);

const rightPaginationButton = ref(3);

const filteredData = ref(props.data);

const currentSubTab = ref(props.selectedSubTab);

const filterTableData = (subTab) => {
  filteredData.value = props.data.filter(
    (element) => element?.subTab == subTab
  );
  calculatePages();
};

watch(
  () => pagination.currentPage,
  (newValue, oldValue) => {
    filteredData.value = props.data.slice(
      (pagination.currentPage - 1) * props.row,
      pagination.currentPage * props.row + 2
    );
  }
);

watch(
  () => props.data,
  () => {
    calculatePages();
    filteredData.value = props.data;
  }
);

onMounted(() => {
  calculatePages();
});

const calculatePages = () => {
  if (props.isPaginated) {
    pagination.currentPage = 1;
    leftPaginationButton.value = 1;
    midPaginationButton.value = 2;
    rightPaginationButton.value = 3;

    const totalDataPages = Math.ceil(filteredData.value.length / props.row);
    pagination.maxPages = totalDataPages;
  }
};

const previousPage = () => {
  if (pagination.currentPage == leftPaginationButton.value) {
    leftPaginationButton.value = leftPaginationButton.value - 3;
    midPaginationButton.value = midPaginationButton.value - 3;
    rightPaginationButton.value = rightPaginationButton.value - 3;
  }

  pagination.currentPage = pagination.currentPage - 1;
};

const nextPage = () => {
  if (pagination.currentPage === rightPaginationButton.value) {
    leftPaginationButton.value = leftPaginationButton.value + 3;
    midPaginationButton.value = midPaginationButton.value + 3;
    rightPaginationButton.value = rightPaginationButton.value + 3;
  }

  pagination.currentPage = pagination.currentPage + 1;
};

const toSelectedPage = (event) => {
  pagination.currentPage = parseInt(event.target.innerHTML);
};

const isNextButtonDisabled = computed(() => {
  return (
    pagination.currentPage === pagination.maxPages || pagination.maxPages === 0
  );
});

const isPreviousButtonDisabled = computed(() => {
  return pagination.currentPage === 1;
});

const changeSubTab = (e) => {
  currentSubTab.value = e;

  filterTableData(e);
};

onMounted(() => {
  columns.value =
    slots.default?.().filter((vnode) => vnode.type.__name === "Column") || [];

  if (props.selectedSubTab) {
    filterTableData(props.selectedSubTab);
  }
});
</script>

<template>
  <div class="shadowAllBorder block overflow-x-auto my-6 rounded-lg scrollbar">
    <table class="w-full">
      <thead class="text-[14px] laptops:text-[16px]">
        <tr v-if="subTabs.length > 0">
          <th colspan="12">
            <div class="flex justify-around divide-x-2">
              <p
                @click="changeSubTab(subtab.name)"
                class="w-full py-4 cursor-pointer hover:shadow-fxblue hover:text-fxblue shadow-[inset_0_-5px_0px_fxblue]"
                v-for="(subtab, index) in subTabs"
                :key="index"
                :class="
                  subtab.name === currentSubTab
                    ? 'shadow-fxblue text-fxblue bg-white'
                    : 'bg-[#f4f4f4]'
                "
              >
                {{
                  t(`${translationPath}.subtabs.${subtab.name.toLowerCase()}`)
                }}
              </p>
            </div>
          </th>
        </tr>
        <tr
          class="border-[#505050] border-b-2 border-opacity-50 h-[64px]"
          :class="theadStyle"
        >
          <th
            v-for="column in columns"
            :key="column.props.field"
            class="capitalize text-fxblue py-4"
          >
            {{ t(`${translationPath}.${column.props.field}`) }}
          </th>
        </tr>
      </thead>
      <tbody class="font-[500] text-[14px] bg-[#f2f2f2]">
        <tr
          v-for="index in row"
          :class="[
            oddColorChange &&
            (filteredData[index - 1]?.[activePropertyName] == undefined ||
              filteredData[index - 1]?.[activePropertyName])
              ? index % 2 != 0
                ? 'bg-white'
                : 'bg-[#f8f9ff]'
              : null,
            {
              'hover:bg-slate-100':
                oddColorChange &&
                (filteredData[index - 1]?.[activePropertyName] ||
                  filteredData[index - 1]?.[activePropertyName] == undefined),
            },
            {
              'opacity-40':
                !filteredData[index - 1]?.[activePropertyName] &&
                filteredData[index - 1]?.[activePropertyName] != undefined,
            },
          ]"
          :key="index"
          class="border-b-2 h-[64px]"
        >
          <slot :value="filteredData[index - 1]"> </slot>
        </tr>
      </tbody>

      <tfoot class="bg-white">
        <tr>
          <td colspan="12" class="h-[64px]">
            <div class="flex justify-center" v-if="isPaginated">
              <div
                class="border border-[#687684] flex rounded-lg text-[#687684] select-none divide-x divide-[#687684]"
              >
                <button
                  :disabled="isPreviousButtonDisabled"
                  @click="previousPage"
                  class="rounded-l-lg px-2"
                  :class="pagination.currentPage == 1 ? 'bg-[#e4e4e4]' : null"
                >
                  <SVGComponent
                    :svgURL="'/img/misc/arrowDropdown.svg'"
                    width="10"
                    heigth="8"
                    :isStroke="true"
                    class="rotate-90"
                    :color="'#687684'"
                  />
                </button>

                <button
                  @click="toSelectedPage"
                  class="px-2"
                  :class="
                    leftPaginationButton == pagination.currentPage
                      ? 'bg-fxblue text-white'
                      : null
                  "
                >
                  {{ leftPaginationButton }}</button
                ><button
                  @click="toSelectedPage"
                  v-if="midPaginationButton <= pagination.maxPages"
                  class="px-2"
                  :class="
                    midPaginationButton == pagination.currentPage
                      ? 'bg-fxblue text-white'
                      : null
                  "
                >
                  {{ midPaginationButton }}
                </button>
                <button
                  @click="toSelectedPage"
                  v-if="rightPaginationButton <= pagination.maxPages"
                  class="px-2"
                  :class="
                    rightPaginationButton == pagination.currentPage
                      ? 'bg-fxblue text-white'
                      : null
                  "
                >
                  {{ rightPaginationButton }}
                </button>

                <button
                  :disabled="isNextButtonDisabled"
                  @click="nextPage"
                  class="px-2 rounded-r-lg"
                  :class="isNextButtonDisabled ? 'bg-[#e4e4e4]' : null"
                >
                  <SVGComponent
                    :svgURL="'/img/misc/arrowDropdown.svg'"
                    width="10"
                    heigth="8"
                    :isStroke="true"
                    class="-rotate-90"
                    :color="'#687684'"
                  />
                </button>
              </div>
            </div>
          </td>
        </tr>
      </tfoot>
    </table>
  </div>
</template>

<style scoped>
.shadowAllBorder {
  box-shadow: 1px 0px 21px 10px rgba(158, 142, 142, 0.21);
  -webkit-box-shadow: 1px 0px 21px 10px rgba(158, 142, 142, 0.21);
  -moz-box-shadow: 1px 0px 21px 10px rgba(158, 142, 142, 0.21);
}

.scrollbar::-webkit-scrollbar-thumb {
  background-color: rgba(0, 0, 0, 0.5);
  border-radius: 10px;
  border: 2px solid #ffffff;
}

.scrollbar::-webkit-scrollbar {
  height: 10px;
}
</style>
