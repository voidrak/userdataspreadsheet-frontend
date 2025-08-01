<script setup>
import { ref } from "vue";

// Form data matching API structure
const formData = ref({
  date: "16/10/2017ዓ.ም",
  number: "216",
  vehicle_owner: "አሰር ኮንስትራክሽን ሃላ/የተ/የግ/ማህበር",
  vehicle_institution: "አሰር ኮንስትራክሽን ሃላ/የተ/የግ/ማህበር",
  vehicle_type: "የመስክ ተሽከርካሪ",
  vehicle_plate_number: "አአ-03-B83219",
  permit_reason: "ከደህንነት አንጻር",
  permit_duration: "ከ28/01/2017ዓ/ም እስከ 27/01/2018ዓ/ም",
  receipt_number: "TT2428ZOCOP",
});

// Sidebar visibility
const sidebarOpen = ref(false);
const isSubmitting = ref(false);

const toggleSidebar = () => {
  sidebarOpen.value = !sidebarOpen.value;
};

// Submit form
const submitForm = async () => {
  isSubmitting.value = true;
  try {
    const response = await fetch(
      "https://userdataspreadsheet-production.up.railway.app/api/post-users",
      {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          vehicle_owner: formData.value.vehicle_owner,
          vehicle_institution: formData.value.vehicle_institution,
          vehicle_type: formData.value.vehicle_type,
          vehicle_plate_number: formData.value.vehicle_plate_number,
          permit_reason: formData.value.permit_reason,
          permit_duration: formData.value.permit_duration,
          receipt_number: formData.value.receipt_number,
        }),
      }
    );

    if (response.ok) {
      const result = await response.json();
      alert("Data submitted successfully!");
      console.log("Success:", result);
    } else {
      throw new Error("Failed to submit data");
    }
  } catch (error) {
    console.error("Error:", error);
    alert("Error submitting data. Please try again.");
  } finally {
    isSubmitting.value = false;
  }
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
        'absolute lg:relative top-0 left-0 h-full bg-white shadow-lg z-40 transition-transform duration-300 ease-in-out',
        sidebarOpen ? 'translate-x-0' : '-translate-x-full',
        'w-80 lg:w-1/3 max-w-[370px]',
      ]"
    >
      <div class="p-6 overflow-y-auto h-full">
        <h2 class="text-xl font-bold mb-6 mt-12 lg:mt-0">
          Vehicle Information Form
        </h2>

        <form @submit.prevent="submitForm" class="space-y-4">
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
            <label class="block text-sm font-medium mb-1">Vehicle Owner</label>
            <input
              v-model="formData.vehicle_owner"
              type="text"
              class="w-full p-2 border rounded"
              required
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1"
              >Vehicle Institution</label
            >
            <input
              v-model="formData.vehicle_institution"
              type="text"
              class="w-full p-2 border rounded"
              required
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1">Vehicle Type</label>
            <input
              v-model="formData.vehicle_type"
              type="text"
              class="w-full p-2 border rounded"
              required
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1"
              >Vehicle Plate Number</label
            >
            <input
              v-model="formData.vehicle_plate_number"
              type="text"
              class="w-full p-2 border rounded"
              required
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1">Permit Reason</label>
            <input
              v-model="formData.permit_reason"
              type="text"
              class="w-full p-2 border rounded"
              required
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1"
              >Permit Duration</label
            >
            <input
              v-model="formData.permit_duration"
              type="text"
              class="w-full p-2 border rounded"
              required
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1">Receipt Number</label>
            <input
              v-model="formData.receipt_number"
              type="text"
              class="w-full p-2 border rounded"
              required
            />
          </div>

          <button
            type="submit"
            :disabled="isSubmitting"
            class="w-full bg-blue-600 text-white py-2 px-4 rounded hover:bg-blue-700 disabled:bg-blue-400 transition-colors"
          >
            {{ isSubmitting ? "Submitting..." : "Submit" }}
          </button>
        </form>
      </div>
    </div>

    <!-- Document Preview Section -->
    <div
      :class="[
        'flex-1 flex justify-center -translate-x-16 mt-16 p-6  transition-all duration-300',
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
          class="absolute left-1/2 -translate-x-1/2 top-1 w-32 h-32 object-contain bg-white rounded-full border-2 border-white z-10"
        />

        <!-- Top right info -->
        <div class="absolute right-8 top-8 text-right text-sm leading-tight">
          <div>ቀን፡ {{ formData.date }}</div>
          <div>
            No: <span class="font-bold mr-16 mt-1">{{ formData.number }}</span>
          </div>
        </div>

        <!-- Headings -->
        <div class="text-center mt-32 mb-2 underline">
          <div class="font-bold text-lg">
            በአዲስ አበባ ከተማ አስተዳደር የትራፊክ ማኔጅመንት ባለስልጣን
          </div>
          <div class="font-bold text-lg">በተሽከርካሪ ላይ የሚለጠፍ የስቲከር ፈቃድ</div>
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
        <ol
          class="relative z-10 text-lg font-sans leading-7 mt-2 ml-8 list-decimal"
        >
          <li>
            <span class="font-bold">ፈቃድ ጠያቂው ተሽከርካሪ ባለንብረት:</span>
            <span class="underline">{{ formData.vehicle_owner }}</span>
          </li>
          <li>
            <span class="font-bold">ፈቃድ ጠያቂው ተሽከርካሪ ተቋም፡</span>
            {{ formData.vehicle_institution }}
          </li>
          <li>
            <span class="font-bold">የተሽከርካሪው አይነት፡</span>
            <span class="underline">{{ formData.vehicle_type }}</span>
          </li>
          <li>
            <span class="font-bold">የተሽከርካሪው ሠሌዳ ቁጥር፡</span>
            <span class="underline">{{ formData.vehicle_plate_number }}</span>
          </li>
          <li>
            <span class="font-bold">ፈቃዱ የተሰጠበት ምክንያት፡</span>
            <span class="underline">{{ formData.permit_reason }}</span>
          </li>
          <li>
            <span class="font-bold">ፈቃዱ የሚያገለግልበት ጊዜ፡</span>
            <span class="underline">{{ formData.permit_duration }}</span>
          </li>
          <li>
            <span class="font-bold">የአገልግሎት ክፍያ የተፈፀመበት ደረሰኝ ቁጥር፡</span>
            <span class="underline">{{ formData.receipt_number }}</span>
          </li>
        </ol>
        <!-- Header text before numbered list -->
        <div class="relative z-10 text-sn font-sans mt-1 font-bold ml-8 mb-2">
          <!-- Stamp image -->
          <img
            src="/stamp.png"
            alt="Official Stamp"
            class="w-22 h-22 object-contain mb-2 absolute -top-6 left-40"
          />
          <div>የፈቃድ ስጪው ስምና ፊርማ፡</div>
        </div>

        <!-- Footer notes -->
        <div class="ml-8 text-sm leading-tight">
          <div class="font-bold mb-1">ማስታወሻ፡</div>
          <ul class="ml-6">
            <li class="flex items-start">
              <span class="mr-2 mt-1">➤</span>
              <span
                >ይህ ፈቃድ የባለስልጣኑ ክብ ማህተም፡ የፈቃድ ስጪው ስምና ፊርማ ከሌለው ወይም ድልዝ ካለበት
                አያገለግልም፡፡</span
              >
            </li>
            <li class="flex items-start">
              <span class="mr-2 mt-1">➤</span>
              <span>የፈቃድ ጊዜው ሲያብቃ በድጋሚ አገልግሎት ለማግኘት ኦርጅናሉ ፈቃድ መመለስ አለበት፡፡</span>
            </li>
            <li class="flex items-start">
              <span class="mr-2 mt-1">➤</span>
              <span
                >የፈቃዱን ከላይ ከተጠቀሰው ተሽከርካሪ ውጪ ከልላ ተሽከርካሪ መጠቀም በፍጹም የተከለከለ ነው</span
              >
            </li>
            <li class="flex items-start">
              <span class="mr-2 mt-1">➤</span>
              <span
                >የስቲከር ፍቃዱን የለጠፈው አሽከርካሪ ለትራፊክ ተቆጣጣሪዎች እና ለትራፊክ ፖሊሶች ፈቃዱን የማሳየት
                ግዴታ አለበት</span
              >
            </li>
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
