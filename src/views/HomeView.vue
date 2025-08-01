<script setup>
import { ref } from "vue";

// Form data
const formData = ref({
  date: "16/10/2017ዓ.ም",
  number: "216",
  ownerName: "አቶ ካሳ ደምሳ",
  driverName: "አቶ ካሳ ደምሳ",
  vehicleType: "ሶፍት-ትዮታ",
  plateNumber: "አን-02-B94700",
  vehicleModel: "ከርሲት አንድ",
  vehicleYear: "የተሽከርካሪ ዓመት ማህበረሰብ የሚሰጥበት",
  ticketStartDate: "16/11/2017ዓ.ም",
  ticketEndDate: "15/11/2018ዓ.ም",
  ticketNumber: "FT25128Z9JQR",
});

// Sidebar visibility
const sidebarOpen = ref(true);

const toggleSidebar = () => {
  sidebarOpen.value = !sidebarOpen.value;
};
</script>

<template>
  <div class="flex min-h-screen bg-gray-100 relative">
    <!-- Toggle Button -->
    <button
      @click="toggleSidebar"
      class="fixed top-4 right-4 z-50 bg-blue-600 text-white p-2 rounded-md shadow-lg hover:bg-blue-700 transition-colors"
    >
      <svg
        v-if="!sidebarOpen"
        class="w-6 h-6"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M4 6h16M4 12h16M4 18h16"
        />
      </svg>
      <svg
        v-else
        class="w-6 h-6"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M6 18L18 6M6 6l12 12"
        />
      </svg>
    </button>

    <!-- Sidebar Overlay (for mobile) -->
    <div
      v-if="sidebarOpen"
      @click="toggleSidebar"
      class="fixed inset-0 bg-black bg-opacity-50 z-30 lg:hidden"
    ></div>

    <!-- Form Sidebar -->
    <div
      :class="[
        'fixed lg:relative top-0 left-0   h-full bg-white shadow-lg z-40 transition-transform duration-300 ease-in-out',
        sidebarOpen ? 'translate-x-0' : '-translate-x-full',
        'w-80 lg:w-1/3',
      ]"
    >
      <div class="p-6 overflow-y-auto h-full">
        <h2 class="text-xl font-bold mb-6 mt-12 lg:mt-0">
          Vehicle Information Form
        </h2>

        <form class="space-y-4">
          <div>
            <label class="block text-sm font-medium mb-1">Date</label>
            <input
              v-model="formData.date"
              type="text"
              class="w-full p-2 border rounded"
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1">Number</label>
            <input
              v-model="formData.number"
              type="text"
              class="w-full p-2 border rounded"
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1">Owner Name</label>
            <input
              v-model="formData.ownerName"
              type="text"
              class="w-full p-2 border rounded"
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1">Driver Name</label>
            <input
              v-model="formData.driverName"
              type="text"
              class="w-full p-2 border rounded"
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1">Vehicle Type</label>
            <input
              v-model="formData.vehicleType"
              type="text"
              class="w-full p-2 border rounded"
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1">Plate Number</label>
            <input
              v-model="formData.plateNumber"
              type="text"
              class="w-full p-2 border rounded"
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1">Vehicle Model</label>
            <input
              v-model="formData.vehicleModel"
              type="text"
              class="w-full p-2 border rounded"
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1">Vehicle Year</label>
            <input
              v-model="formData.vehicleYear"
              type="text"
              class="w-full p-2 border rounded"
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1"
              >Ticket Start Date</label
            >
            <input
              v-model="formData.ticketStartDate"
              type="text"
              class="w-full p-2 border rounded"
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1"
              >Ticket End Date</label
            >
            <input
              v-model="formData.ticketEndDate"
              type="text"
              class="w-full p-2 border rounded"
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1">Ticket Number</label>
            <input
              v-model="formData.ticketNumber"
              type="text"
              class="w-full p-2 border rounded"
            />
          </div>
        </form>
      </div>
    </div>

    <!-- Document Preview Section -->
    <div
      :class="[
        'flex-1 flex justify-center -translate-x-32 items-center p-6 transition-all duration-300',
        sidebarOpen ? 'lg:ml-0' : 'ml-0',
      ]"
    >
      <div
        class="bg-white border-4 border-black p-8 relative w-[900px] h-[600px] mx-auto"
      >
        <!-- Logo -->
        <img
          src="/logo.webp"
          alt="Logo"
          class="absolute left-1/2 -translate-x-1/2 top-4 w-28 h-28 object-contain bg-white rounded-full border-2 border-white z-10"
        />

        <!-- Top right info -->
        <div class="absolute right-8 top-8 text-right text-sm leading-tight">
          <div>ቀን፡ {{ formData.date }}</div>
          <div>
            No: <span class="font-bold">{{ formData.number }}</span>
          </div>
        </div>

        <!-- Headings -->
        <div class="text-center mt-32 mb-2">
          <div class="font-bold text-lg">የእንቅስቃሴ እና ተሽከርካሪ ትኬት ማስታወቂያ በሰሌዳ</div>
          <div class="font-bold text-lg">
            በተሽከርካሪ ባለ የሚሰጥበት የትኬት ማስታወቂያ ደብዳቤ
          </div>
        </div>

        <!-- Vehicle image background -->
        <img
          src="/car.png"
          alt="Car"
          class="absolute left-0 top-24 w-full h-[320px] object-contain opacity-40 z-0"
        />

        <!-- QR code -->
        <img
          src="/qr.png"
          alt="QR Code"
          class="absolute right-16 top-56 w-32 h-32 bg-white p-2 z-10 border border-black"
        />

        <!-- Numbered list -->
        <ol class="relative z-10 text-lg font-sans leading-7 mt-2 ml-2">
          <li>
            <span class="font-bold">የተሽከርካሪ ባለቤት ትኬት ባለቤት፡</span>
            {{ formData.ownerName }}
          </li>
          <li>
            <span class="font-bold">የተሽከርካሪ አሽከርካሪ ስም፡</span>
            {{ formData.driverName }}
          </li>
          <li>
            <span class="font-bold">ተሽከርካሪ አይነት፡</span>
            {{ formData.vehicleType }}
          </li>
          <li>
            <span class="font-bold">ተሽከርካሪ የምዝገባ ቁጥር፡</span>
            {{ formData.plateNumber }}
          </li>
          <li>
            <span class="font-bold">የተሽከርካሪ ምልክት፡</span>
            {{ formData.vehicleModel }}
          </li>
          <li>
            <span class="font-bold">የተሽከርካሪ ቀን፡</span>
            {{ formData.vehicleYear }}
          </li>
          <li>
            <span class="font-bold">የትኬት ማስታወቂያ ቀን፡</span>
            {{ formData.ticketStartDate }} እስከ {{ formData.ticketEndDate }}
          </li>
          <li>
            <span class="font-bold">የትኬት ማስታወቂያ ቁጥር፡</span>
            {{ formData.ticketNumber }}
          </li>
        </ol>

        <!-- Footer notes -->
        <div class="absolute left-8 bottom-8 right-8 text-sm leading-tight">
          <div class="font-bold mb-1">ማስታወሻ፡</div>
          <ul class="list-disc ml-6">
            <li>ይህ ደብዳቤ በማህበረሰቡ በሚሰጥበት ቦታ ብቻ የሚሰጥ ነው፡፡</li>
            <li>ይህን ደብዳቤ በማህበረሰቡ ቦታ ማስታወቂያ እንደሚሰጥ ይህን ደብዳቤ ይያዙ፡፡</li>
            <li>ይህን ደብዳቤ በማህበረሰቡ ቦታ ማስታወቂያ እንደሚሰጥ ይያዙ፡፡</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Optional: custom font for Amharic if needed */
/* @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Ethiopic:wght@400;700&display=swap');
.font-sans { font-family: 'Noto Sans Ethiopic', sans-serif; } */
</style>
