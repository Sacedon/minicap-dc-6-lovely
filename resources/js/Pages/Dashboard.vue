<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';

</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
      <div class="py-12 fade-in">
        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
          <div class="bg-white dark:bg-green-700 overflow-hidden shadow-sm sm:rounded-lg">

            <!-- Header -->
            <div class="p-6 text-gray-900 dark:text-gray-100">
              <h1 class="text-2xl font-semibold">Plant Dashboard</h1>
              <p class="text-sm">Welcome to your plant dashboard. Here's an overview of your plants and their health.</p>
            </div>

            <hr>

            <!-- Statistics Section -->
            <div class="p-6">
              <div class="grid grid-cols-2 gap-4">
                <div class="bg-blue-100 p-4 rounded-lg shadow-md">
                  <h2 class="text-lg font-semibold">Total Plants</h2>
                  <p class="text-xl font-bold">50</p>
                </div>
                <div class="bg-green-100 p-4 rounded-lg shadow-md">
                  <h2 class="text-lg font-semibold">Healthy Plants</h2>
                  <p class="text-xl font-bold">45</p>
                </div>
                <div class="bg-red-100 p-4 rounded-lg shadow-md">
                  <h2 class="text-lg font-semibold">Unhealthy Plants</h2>
                  <p class="text-xl font-bold">5</p>
                </div>
                <div class="bg-yellow-100 p-4 rounded-lg shadow-md">
                  <h2 class="text-lg font-semibold">Plants Needing Water</h2>
                  <p class="text-xl font-bold">8</p>
                </div>
              </div>
            </div>

            <hr>

            <!-- Plant List Section -->
            <div class="p-6">
              <h2 class="text-lg font-semibold">Plant List</h2>
              <!-- Add a list of your plants here -->
              <ul class="list-disc pl-6">
                <li>Plant 1 - Healthy</li>
                <li>Plant 2 - Unhealthy</li>
                <li>Plant 3 - Needs Water</li>
                <!-- Add more plant entries as needed -->
              </ul>
            </div>

            <hr>

            <!-- Additional Dashboard Widgets -->
            <div class="p-6">
              <h2 class="text-lg font-semibold">Additional Widgets</h2>
              <!-- Add more widgets and content here -->
              <div class="mt-4">
                <div class="bg-purple-100 p-4 rounded-lg shadow-md">
                  <h3 class="text-lg font-semibold">Temperature</h3>
                  <p class="text-xl font-bold">25°C</p>
                </div>
              </div>
            </div>

          </div>
        </div>
      </div>
    </AuthenticatedLayout>
  </template>



<style>
    @keyframes fadeIn {
        from {
            opacity: 0;
        }
        to {
            opacity: 1;
        }
    }

    .fade-in {
        animation: fadeIn 0.3s ease-in-out; /* Adjust the duration and timing function as needed */
    }
</style>
