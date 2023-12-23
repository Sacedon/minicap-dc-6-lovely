<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import { inject, ref } from 'vue';
import Card from '@/Components/Card.vue';

// Use 'discount' as the default value if 'discountValue' is not provided
const discountValue = inject('discountValue');
</script>

<template>
    <Head title="Dashboard" />



    <AuthenticatedLayout>
        <div class="py-12 fade-in">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white dark:bg-green-600 overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 text-gray-900 dark:text-gray-100">
                    <!-- Loop All Plugins Created / Tailwind Modal Create / Tailwind Modal Edit / Tailwind Modal Delete -->

                    <div v-for="discount in discounts" :key="discount.id">
                        <p class=""><b><i class="fa-solid fa-tag"></i> Discount:</b> ${{ discount.discount }}</p>
                    </div>
                    <div class="flex justify-end" style="margin-top: -30px;">
                        <!-- <button> Discount </button> -->

                        <button @click="openCreateModal" class="bg-blue-600 p-3 rounded-lg hover:bg-blue-800 duration-200"> Add</button>

                    </div>

                    <div>
                        <header style="font-size: 30px;"><i class="fa-brands fa-pagelines"></i> Plants Management</header>
                    </div> <br>
                    <div>
                        <!-- Loop All Plugin -->
                        <div class="">
                            <form @submit.prevent="submitFilter" class="flex flex-wrap items-center space-y-4 sm:space-y-0 sm:space-x-4 mb-5">
  <div class="flex items-center w-full sm:w-auto">
    <label for="startDate" class="mr-2 text-gray-800">Start Date:</label>
    <div class="relative flex items-center w-full max-w-xs">
      <input v-model="startDate" type="date" id="startDate" name="startDate"
        class="text-gray-800 py-2 px-3 border border-gray-300 rounded-md focus:outline-none focus:border-indigo-500 flex-grow">
      <span class="absolute right-3 top-2.5">
        <i class="fas fa-calendar text-gray-400"></i>
      </span>
    </div>
  </div>

  <div class="flex items-center w-full sm:w-auto">
    <label for="endDate" class="mr-2 text-gray-800">End Date:</label>
    <div class="relative flex items-center w-full max-w-xs">
      <input v-model="endDate" type="date" id="endDate" name="endDate"
        class="text-gray-800 py-2 px-3 border border-gray-300 rounded-md focus:outline-none focus:border-indigo-500 flex-grow">
      <span class="absolute right-3 top-2.5">
        <i class="fas fa-calendar text-gray-400"></i>
      </span>
    </div>
  </div>

  <button type="submit"
    class="bg-green-500 hover:bg-geen-700 text-white py-2 px-4 rounded-md flex items-center space-x-2">
    <i class="fas fa-filter text-gray-100"></i>
    <span>Apply Filter</span>
  </button>
</form>


<table class="min-w-full divide-y divide-gray-200">
  <thead>
    <tr>
      <th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">Name</th>
      <th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">Type of Plants</th>
      <th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">Price</th>
      <th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">Description</th>
      <th class="px-6 py-3 bg-gray-50"></th>
    </tr>
  </thead>
  <tbody class="bg-green-700 divide-y divide-gray-200">
    <tr v-for="plugin in plugins" :key="plugin.id">
      <td class="px-6 py-4 whitespace-no-wrap">{{ plugin.name }}</td>
      <td class="px-6 py-4 whitespace-no-wrap">{{ plugin.daws }}</td>
      <td class="px-6 py-4 whitespace-no-wrap">${{ plugin.price }}</td>
      <td class="px-6 py-4 whitespace-no-wrap">{{ plugin.description }}</td>
      <td class="px-6 py-4 whitespace-no-wrap">
        <button @click="openEditModal(plugin)" class="text-indigo-600 hover:text-indigo-900 font-semibold mr-2">Edit</button>
        <button @click="deletePlugin(plugin.id)" class="text-red-600 hover:text-red-900 font-semibold">Delete</button>
      </td>
    </tr>
  </tbody>
</table>









                        </div>
                    </div>

                    <!-- Create Modal -->
                    <div v-if="showCreateModal" class="fixed z-50 inset-0 overflow-y-auto flex items-center justify-center min-h-screen">
  <!-- Overlay -->
  <div class="fixed inset-0 bg-black opacity-50"></div>

  <!-- Modal Container -->
  <div class="relative bg-white dark:bg-gray-800 w-96 p-6 rounded-lg shadow-lg text-gray-900 dark:text-gray-400">
    <h2 class="text-3xl font-semibold mb-6">Add Plant</h2>

    <!-- Form for creating a new plugin -->
    <form @submit.prevent="createPlugin">
      <!-- Name -->
      <div class="mb-4">
        <label for="name" class="block text-sm font-medium">Name</label>
        <input
          type="text"
          id="name"
          v-model="newPlugin.name"
          class="w-full px-4 py-2 rounded border border-gray-300 focus:outline-none focus:border-indigo-600 dark:focus:border-indigo-300"
          required
        >
      </div>

      <!-- Description -->
      <div class="mb-4">
        <label for="description" class="block text-sm font-medium">Description</label>
        <textarea
          id="description"
          v-model="newPlugin.description"
          class="w-full px-4 py-2 rounded border border-gray-300 focus:outline-none focus:border-indigo-600 dark:focus:border-indigo-300"
          required
        ></textarea>
      </div>

      <!-- Model -->
      <div class="mb-4">
        <label for="daws" class="block text-sm font-medium">Type of Plant</label>
        <input
          type="text"
          id="daws"
          v-model="newPlugin.daws"
          class="w-full px-4 py-2 rounded border border-gray-300 focus:outline-none focus:border-indigo-600 dark:focus:border-indigo-300"
          required
        >
      </div>

      <!-- Price -->
      <div class="mb-4">
        <label for="price" class="block text-sm font-medium">Price</label>
        <input
          type="number"
          id="price"
          v-model="newPlugin.price"
          class="w-full px-4 py-2 rounded border border-gray-300 focus:outline-none focus:border-indigo-600 dark:focus:border-indigo-300"
          required
        >
      </div>

      <!-- Actions -->
      <div class="flex justify-end">
        <button @click="closeCreateModal" class="bg-gray-600 hover:bg-gray-700 text-white px-4 py-2 rounded-full mr-2">Close</button>

        <button type="submit" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2 rounded-full">Add</button>
      </div>
    </form>
  </div>
</div>




                    <!-- Edit Modal -->
                    <div v-if="showEditModal" class="fixed inset-0 flex items-center justify-center overflow-y-auto z-50">
  <!-- Overlay -->
  <div class="fixed inset-0 bg-black opacity-50"></div>

  <!-- Modal Container -->
  <div class="relative bg-white dark:bg-gray-800 w-96 p-6 rounded-lg shadow-lg text-gray-900 dark:text-gray-400">
    <h2 class="text-3xl font-semibold mb-6">Edit Plant</h2>

    <!-- Form for editing an existing plugin -->
    <form @submit.prevent="updatePlugin">
      <!-- Name -->
      <div class="mb-4">
        <label for="name" class="block text-sm font-medium">Name</label>
        <input
          type="text"
          id="name"
          v-model="editPlugin.name"
          class="w-full px-4 py-2 rounded border border-gray-300 focus:outline-none focus:border-indigo-600 dark:focus:border-indigo-300"
          required
        >
      </div>

      <!-- Description -->
      <div class="mb-4">
        <label for="description" class="block text-sm font-medium">Description</label>
        <textarea
          id="description"
          v-model="editPlugin.description"
          class="w-full px-4 py-2 rounded border border-gray-300 focus:outline-none focus:border-indigo-600 dark:focus:border-indigo-300"
          required
        ></textarea>
      </div>

      <!-- Model -->
      <div class="mb-4">
        <label for="daws" class="block text-sm font-medium">Type of Plant</label>
        <input
          type="text"
          id="daws"
          v-model="editPlugin.daws"
          class="w-full px-4 py-2 rounded border border-gray-300 focus:outline-none focus:border-indigo-600 dark:focus:border-indigo-300"
          required
        >
      </div>

      <!-- Price -->
      <div class="mb-4">
        <label for="price" class="block text-sm font-medium">Price</label>
        <input
          type="number"
          id="price"
          v-model="editPlugin.price"
          class="w-full px-4 py-2 rounded border border-gray-300 focus:outline-none focus:border-indigo-600 dark:focus:border-indigo-300"
          required
        >
      </div>

      <!-- Actions -->
      <div class="flex justify-end">
        <button @click="closeEditModal" class="bg-gray-600 hover:bg-gray-700 text-white px-4 py-2 rounded-full mr-2">Close</button>

        <button type="submit" class="bg-blue-600 hover:bg-blue-800 text-white px-4 py-2 rounded-full">Update</button>
      </div>
    </form>
  </div>
</div>




                    </div>
                    <br>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
<script>
export default {
    props: {
        plugins: Array,
        discounts: Array,

    },
    data() {
        return {
            showCreateModal: false,
            showEditModal: false,
            showDeleteModal: false,
            selectedPlugin: null,
            showCreateModal: false,
            startDate: '',
            endDate: '',
            newPlugin: {
                name: '',
                description: '',
                daws: '',
                price: '',

            },
                editPlugin: {
                id: null,
                name: '',
                description: '',
                daws: '',
                price: 0,
            },
        };

    },

    computed: {
        filteredPlugins() {
            // Implement the logic to filter plugins based on start and end dates
            if (this.startDate && this.endDate) {
                const startTimestamp = new Date(this.startDate).getTime();
                const endTimestamp = new Date(this.endDate).getTime();

                return this.plugins.filter(plugin => {
                    const pluginDate = new Date(plugin.date).getTime();
                    return pluginDate >= startTimestamp && pluginDate <= endTimestamp;
                });
            } else {
                // Return all plugins if no date range is specified
                return this.plugins;
            }
        },
    },

    methods: {
        openCreateModal() {
            this.showCreateModal = true;
        },
        closeCreateModal() {
            this.showCreateModal = false;
        },

        openEditModal(plugin) {
            this.showEditModal = true;
            this.editPlugin = { ...plugin }; // Create a copy of the plugin details
        },
        closeEditModal() {
            this.showEditModal = false;
        },
        updatePlugin() {
            this.$inertia.put(`/plugins/${this.editPlugin.id}`, this.editPlugin).then(() => {
                this.closeEditModal();
            }).catch(error => {
                console.error('Error updating plugin:', error);
            });
        },
        openDeleteModal(pluginId) {
            this.selectedPluginId = pluginId;
            this.showDeleteModal = true;
        },
        closeDeleteModal() {
            this.selectedPluginId = null;
            this.showDeleteModal = false;
        },
        deletePlugin() {
            // Add logic to delete the selected plugin
            this.closeDeleteModal();
        },

        createPlugin() {
            this.$inertia.post('/plugins', this.newPlugin).then(() => {
                this.closeCreateModal();
            });
        },

        deletePlugin(pluginId) {
            if (confirm("Are you sure you want to delete this plant?")) {
                this.$inertia.delete(`/plugins/${pluginId}`).then(() => {
                    // Optionally, you can fetch the updated data from the server and update the local state
                    // Example: this.fetchPluginData();

                    // You can also close the modal or perform other actions as needed
                }).catch(error => {
                    // Handle error if the delete request fails
                    console.error('Error deleting plugin:', error);
                });
            }
        },


        submitFilter() {
            // Fetch and update plugins based on the selected date range
            // You can make an Inertia request to your Laravel backend here
            this.$inertia.get('/plugins', { startDate: this.startDate, endDate: this.endDate }).then(response => {
                // Update the plugins with the response
                this.$emit('update-plugins', response.plugins);

                // Close the filter form or perform any other actions
            });
        },

    },
};
</script>
