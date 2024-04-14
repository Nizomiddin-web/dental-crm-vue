<script setup>
import { onMounted, reactive, ref, watch } from "vue";
import { ProductService } from "@/service/ProductService";
import { useLayout } from "@/layout/composables/layout";
import PatientChart from "../components/PatientChart.vue"
import Chart from 'primevue/chart';


const { isDarkTheme } = useLayout();

const products = ref(null);
const lineData = reactive({
  labels: ["January", "February", "March", "April", "May", "June", "July"],
  datasets: [
    {
      label: "First Dataset",
      data: [65, 59, 80, 81, 56, 55, 40],
      fill: false,
      backgroundColor: "#2f4860",
      borderColor: "#2f4860",
      tension: 0.4,
    },
    {
      label: "Second Dataset",
      data: [28, 48, 40, 19, 86, 27, 90],
      fill: false,
      backgroundColor: "#00bb7e",
      borderColor: "#00bb7e",
      tension: 0.4,
    },
  ],
});
const items = ref([
  { label: "Add New", icon: "pi pi-fw pi-plus" },
  { label: "Remove", icon: "pi pi-fw pi-minus" },
]);
const lineOptions = ref(null);
const productService = new ProductService();


onMounted(() => {
    chartData.value = setChartData();
    chartOptions.value = setChartOptions();
});

const chartData = ref();
const chartOptions = ref();

const setChartData = () => {
    const documentStyle = getComputedStyle(document.body);

    return {
        labels: ['Ayol', 'Erkak'],
        datasets: [
            {
                data: [600,540],
                backgroundColor: [documentStyle.getPropertyValue('--cyan-500'), documentStyle.getPropertyValue('--orange-500'), documentStyle.getPropertyValue('--gray-500')],
                hoverBackgroundColor: [documentStyle.getPropertyValue('--cyan-400'), documentStyle.getPropertyValue('--orange-400'), documentStyle.getPropertyValue('--gray-400')]
            }
        ]
    };
};

const setChartOptions = () => {
    const documentStyle = getComputedStyle(document.documentElement);
    const textColor = documentStyle.getPropertyValue('--text-color');

    return {
        plugins: {
            legend: {
                labels: {
                    usePointStyle: true,
                    color: textColor
                }
            }
        }
    };
};

onMounted(() => {
  productService.getProductsSmall().then((data) => (products.value = data));
});

const formatCurrency = (value) => {
  return value.toLocaleString("en-US", { style: "currency", currency: "USD" });
};
const applyLightTheme = () => {
  lineOptions.value = {
    plugins: {
      legend: {
        labels: {
          color: "#495057",
        },
      },
    },
    scales: {
      x: {
        ticks: {
          color: "#495057",
        },
        grid: {
          color: "#ebedef",
        },
      },
      y: {
        ticks: {
          color: "#495057",
        },
        grid: {
          color: "#ebedef",
        },
      },
    },
  };
};

const applyDarkTheme = () => {
  lineOptions.value = {
    plugins: {
      legend: {
        labels: {
          color: "#ebedef",
        },
      },
    },
    scales: {
      x: {
        ticks: {
          color: "#ebedef",
        },
        grid: {
          color: "rgba(160, 167, 181, .3)",
        },
      },
      y: {
        ticks: {
          color: "#ebedef",
        },
        grid: {
          color: "rgba(160, 167, 181, .3)",
        },
      },
    },
  };
};

watch(
  isDarkTheme,
  (val) => {
    if (val) {
      applyDarkTheme();
    } else {
      applyLightTheme();
    }
  },
  { immediate: true }
);
</script>

<template>
  <div class="grid">
    <div class="col-12 lg:col-6 xl:col-3 ">
      <div class="card mb-0">
        <div class="flex justify-content-between mb-3">
          <div>
            <span class="block text-500 font-medium mb-3">Yangi Be'morlar</span>
            <div class="text-900 font-medium text-xl">3 ta</div>
          </div>
          <div
            class="flex align-items-center justify-content-center bg-cyan-100 border-round"
            style="width: 2.5rem; height: 2.5rem;"
          >
            <i class="pi pi-users text-cyan-500 text-xl"></i>
          </div>
        </div>
        <span class="text-cyan-500 font-medium"></span>
        <span class="text-500">Oxirgi 7 kunlik</span>
      </div>
    </div>
    <div class="col-12 lg:col-6 xl:col-3 ">
      <div class="card mb-0">
        <div class="flex justify-content-between mb-3">
          <div>
            <span class="block text-500 font-medium mb-3">Davolashlar</span>
            <div class="text-900 font-medium text-xl">100 ta</div>
          </div>
          <div
            class="flex align-items-center justify-content-center bg-green-100 border-round"
            style="width: 2.5rem; height: 2.5rem;"
          >
            <i class="pi pi-check-square text-green-500 text-xl"></i>
          </div>
        </div>
        <span class="text-green-500 font-medium">14-aprel</span>
        <span class="text-500"> 2024-yil</span>
      </div>
    </div>
    <div class="col-12 lg:col-6 xl:col-3 ">
      <div class="card mb-0">
        <div class="flex justify-content-between mb-3">
          <div>
            <span class="block text-500 font-medium mb-3">To'lovlar</span>
            <div class="text-900 font-medium text-xl">28441</div>
          </div>
          <div
            class="flex align-items-center justify-content-center bg-cyan-100 border-round"
            style="width: 2.5rem; height: 2.5rem;"
          >
            <i class="pi pi-wallet text-cyan-500 text-xl"></i>
          </div>
        </div>
        <span class="text-green-500 font-medium">14-aprel</span>
        <span class="text-500"> 2024-yil</span>
      </div>
    </div>
    <div class="col-12 lg:col-6 xl:col-3 ">
      <div class="card mb-0">
        <div class="flex justify-content-between mb-3">
          <div>
            <span class="block text-500 font-medium mb-3"
              >Qarzdor be'morlar</span
            >
            <div class="text-900 font-medium text-xl">152 ta</div>
          </div>
          <div
            class="flex align-items-center justify-content-center bg-red-100 border-round"
            style="width: 2.5rem; height: 2.5rem;"
          >
            <i class="pi pi-user-minus text-red-500 text-xl"></i>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="flex gap-3">
    <div class="card flex-row justify-content-center">
        <h6>Bemorlar statistikasi jinsi bo'yicha</h6>
        <Divider />
        <Chart type="pie" :data="chartData" :options="chartOptions" class="w-full md:w-30rem" />
    </div>
    <div class=""><PatientChart/></div>
  </div>
</template>
