<script setup>
import { ref } from 'vue';
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import Dropdown from '@/Components/Dropdown.vue';
import DropdownLink from '@/Components/DropdownLink.vue';
import NavLink from '@/Components/NavLink.vue';
import ResponsiveNavLink from '@/Components/ResponsiveNavLink.vue';
import { Link } from '@inertiajs/vue3';

import { onMounted, provide } from 'vue';
const selectedColor = ref('green'); // Default background color
provide('color', selectedColor)

const showingNavigationDropdown = ref(false);
const sidebarWidth = ref(200); // Initial width of the sidebar
const minSidebarWidth = 64; // Minimum width of the sidebar
const maxSidebarWidth = 200; // Maximum width of the sidebar
const smallSizeThreshold = 100; // Adjust this threshold as needed

const toggleSidebarWidth = () => {
  sidebarWidth.value = sidebarWidth.value === minSidebarWidth ? maxSidebarWidth : minSidebarWidth;
};
</script>



<template>
  <div class="min-h-screen flex bg-gray-100 dark:bg-gray-900">
    <!-- Sidebar -->
    <aside :style="{ width: `${sidebarWidth}px`, transition: 'width 0.5s' }" class="bg-white dark:bg-green-800 border-r border-gray-100 dark:border-gray-700">
      <!-- Resizable Button -->
      <div class="cursor-pointer" @click="toggleSidebarWidth">
        <div class="flex justify-end">
          <button v-if="sidebarWidth <= smallSizeThreshold" style="font-size: 30px;">
            <i class="fa-solid fa-caret-right text-white hover:text-black p-7 duration-100"></i>
          </button>

          <button v-else style="font-size: 30px;">
            <i class="fa-solid fa-caret-left text-white hover:text-black p-5 duration-100"></i>
          </button>
        </div>
      </div>

      <!-- Logo -->
      <div class="mt-5" style="display: grid; place-content: center;">
  <img width="150px" src="data:image/png;base64,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" alt="" style="border-radius: 50%;">
</div>


      <!-- Links -->
      <div class="mt-10" style="display: grid; place-content: center;">
        <!-- Check if sidebarWidth is less than or equal to a threshold for small size -->
        <NavLink v-if="sidebarWidth <= smallSizeThreshold" style="font-size: 25px;" :href="route('dashboard')">
          <i class="fa fa-dashboard"></i>
        </NavLink>

        <!-- Otherwise, show only the icon -->
        <NavLink v-else style="font-size: 20px;" :href="route('dashboard')">
          <div style="width: 150px;"><i class="fa-solid fa-table-columns"></i><span style="margin-left: 10px;">Dashboard</span></div>
        </NavLink>

      </div>





         <!-- Links -->
      <div class="mt-10" style="display: grid; place-content: center;">
        <!-- Check if sidebarWidth is less than or equal to a threshold for small size -->
        <NavLink v-if="sidebarWidth <= smallSizeThreshold" style="font-size: 25px;" :href="route('index')">
          <i class="fa-solid fa-store"></i>
        </NavLink>

        <!-- Otherwise, show only the icon -->
        <NavLink v-else style="font-size: 20px;" :href="route('index')">
          <div style="width: 150px;"><i class="fa-solid fa-tree"></i><span style="margin-left: 7px;">Plants</span></div>
        </NavLink>



      </div>




            <!-- Links -->





       <!-- Links -->
       <div class="mt-10 mb-10" style="display: grid; place-content: center;">
        <!-- Check if sidebarWidth is less than or equal to a threshold for small size -->
        <NavLink v-if="sidebarWidth <= smallSizeThreshold" style="font-size: 25px;" :href="route('dateIndex')">
            <i class="fa-solid fa-calendar"></i>
        </NavLink>

        <!-- Otherwise, show only the icon -->
        <NavLink v-else style="font-size: 20px;" :href="route('dateIndex')">
          <div style="width: 150px;"><i class="fa-regular fa-calendar-plus"></i><span style="margin-left: 7px;">Calendar</span></div>
        </NavLink>






      </div>

      <div>
  <!-- Settings Dropdown -->
  <div class="mt-10 mb-10" style="display: grid; place-content: center;">
    <NavLink style="font-size: 20px;" :href="route('profile.edit')">
     <div style="width: 150;"><span style="margin-left: 7px;"> Profile </span></div>
    </NavLink>
    <NavLink style="font-size: 20px;" :href="route('logout')" method="post" as="button">
      Log Out
    </NavLink>
  </div>
</div>






    </aside>



    <!-- Main Content -->
    <div class="flex-1 flex flex-col overflow-hidden">
      <nav class="bg-white dark:bg-white border-b border-gray-100 dark:border-gray-700">
        <!-- Primary Navigation Menu -->
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div class=" h-16 mt-5">

            <h1 class="text-4xl font-bold text-center bg-gray-100 dark:bg-white py-4 px-6 rounded-lg shadow-md">
        Plant Management
    </h1>




            <!-- Hamburger -->
            <div class="-me-2 flex items-center sm:hidden">
              <button
                @click="showingNavigationDropdown = !showingNavigationDropdown"
                class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 dark:text-gray-500 hover:text-gray-500 dark:hover:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-900 focus:outline-none focus:bg-gray-100 dark:focus:bg-gray-900 focus:text-gray-500 dark:focus:text-gray-400 transition duration-150 ease-in-out"
              >
                <svg class="h-6 w-6" stroke="currentColor" fill="none" viewBox="0 0 24 24">
                  <path
                    :class="{
                      hidden: showingNavigationDropdown,
                      'inline-flex': !showingNavigationDropdown,
                    }"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M4 6h16M4 12h16M4 18h16"
                  />
                  <path
                    :class="{
                      hidden: !showingNavigationDropdown,
                      'inline-flex': showingNavigationDropdown,
                    }"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M6 18L18 6M6 6l12 12"
                  />
                </svg>
              </button>
            </div>
          </div>
        </div>

        <!-- Responsive Navigation Menu -->
        <div
          :class="{ block: showingNavigationDropdown, hidden: !showingNavigationDropdown }"
          class="sm:hidden"
        >
          <div class="pt-2 pb-3 space-y-1">
            <ResponsiveNavLink :href="route('dashboard')" :active="route().current('dashboard')">
              Dashboard
            </ResponsiveNavLink>
          </div>

          <!-- Responsive Settings Options -->
          <div class="pt-4 pb-1 border-t border-gray-200 dark:border-gray-600">
            <div class="px-4">
              <div class="font-medium text-base text-gray-800 dark:text-gray-200">
                {{ $page.props.auth.user.name }}
              </div>
              <div class="font-medium text-sm text-gray-500">{{ $page.props.auth.user.email }}</div>
            </div>

            <div class="mt-3 space-y-1">
              <ResponsiveNavLink :href="route('profile.edit')"> Profile </ResponsiveNavLink>
              <ResponsiveNavLink :href="route('logout')" method="post" as="button">
                Log Out
              </ResponsiveNavLink>
            </div>
          </div>
        </div>
      </nav>

      <!-- Page Heading -->
      <header class="bg-white dark:bg-gray-800 shadow" v-if="$slots.header">
        <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
          <slot name="header" />
        </div>
      </header>

      <!-- Page Content -->
      <main class="flex-1 overflow-x-hidden overflow-y-auto bg-gray-100 dark:bg-green-600">
        <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
          <slot />
        </div>
      </main>
    </div>
  </div>
</template>
