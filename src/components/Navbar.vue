<template>
  <header
    class="flex items-center justify-between h-20 px-4 bg-white border shadow"
  >
    <div class="flex">
      <!-- Logo atau brand -->
      <img src="/public/ngemeals-logo.png" alt="" class="w-40" />
    </div>
    <div
      class="hidden p-2 transition bg-gray-100 rounded-lg md:flex hover:bg-gray-200"
    >
      <nav
        class="flex gap-x-1"
        aria-label="Tabs"
        role="tablist"
        aria-orientation="horizontal"
      >
        <router-link
          :to="{ name: 'home' }"
          class="tab-item"
          role="tab"
          id="segment-item-1"
          aria-selected="true"
          aria-controls="segment-1"
          :class="{ 'bg-white text-gray-700 active': isActive('home') }"
          @click="setActive('home')"
        >
          Home
        </router-link>

        <router-link
          :to="{ name: 'byName' }"
          class="tab-item"
          role="tab"
          id="segment-item-2"
          aria-selected="false"
          aria-controls="segment-2"
          :class="{ 'bg-white text-gray-700 active': isActive('byName') }"
          @click="setActive('byName')"
        >
          Search Meals
        </router-link>

        <router-link
          :to="{ name: 'byLetter' }"
          class="tab-item"
          role="tab"
          id="segment-item-3"
          aria-selected="false"
          aria-controls="segment-3"
          :class="{ 'bg-white text-gray-700 active': isActive('byLetter') }"
          @click="setActive('byLetter')"
        >
          Meals By Letter
        </router-link>

        <router-link
          :to="{ name: 'ingredients' }"
          class="tab-item"
          role="tab"
          id="segment-item-4"
          aria-selected="false"
          aria-controls="segment-4"
          :class="{ 'bg-white text-gray-700 active': isActive('ingredients') }"
          @click="setActive('ingredients')"
        >
          Meals By Ingredients
        </router-link>
      </nav>
    </div>

    <!-- Menu toggle untuk mobile -->
    <button
      class="block p-2 bg-gray-100 rounded-lg md:hidden hover:bg-gray-200 focus:outline-none"
      @click="toggleMenu"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="w-6 h-6 text-gray-700"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M4 6h16M4 12h16m-7 6h7"
        />
      </svg>
    </button>

    <!-- Dropdown menu untuk mobile -->
    <div
      v-if="isMenuOpen"
      class="absolute left-0 z-30 w-full bg-white border shadow-lg top-20"
    >
      <nav class="flex flex-col items-center p-4 gap-y-2">
        <router-link
          :to="{ name: 'home' }"
          class="tab-item"
          :class="{ 'bg-gray-100': isActive('home') }"
          @click="
            setActive('home');
            toggleMenu();
          "
        >
          Home
        </router-link>
        <router-link
          :to="{ name: 'byName' }"
          class="tab-item"
          :class="{ 'bg-gray-100': isActive('byName') }"
          @click="
            setActive('byName');
            toggleMenu();
          "
        >
          Search Meals
        </router-link>
        <router-link
          :to="{ name: 'byLetter' }"
          class="tab-item"
          :class="{ 'bg-gray-100': isActive('byLetter') }"
          @click="
            setActive('byLetter');
            toggleMenu();
          "
        >
          Meals By Letter
        </router-link>
        <router-link
          :to="{ name: 'ingredients' }"
          class="tab-item"
          :class="{ 'bg-gray-100': isActive('ingredients') }"
          @click="
            setActive('ingredients');
            toggleMenu();
          "
        >
          Meals By Ingredients
        </router-link>
      </nav>
    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {
      activeTab: "home", // Default active tab
      isMenuOpen: false, // State untuk menu mobile
    };
  },
  methods: {
    setActive(tab) {
      this.activeTab = tab;
    },
    isActive(tab) {
      return this.activeTab === tab;
    },
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
  },
};
</script>

<style scoped>
.tab-item {
  padding: 12px 24px;
  min-width: 150px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  font-size: 14px;
  color: #6b7280;
  transition: background-color 0.3s ease, color 0.3s ease, transform 0.3s ease;
  border-radius: 8px;
  font-weight: 500;
  margin: 0 4px;
}

.tab-item:hover {
  background-color: #e5e7eb;
  color: #374151;
}

.tab-item.active {
  background-color: #ffffff;
  color: #374151;
  transform: scale(1.05);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}
</style>
